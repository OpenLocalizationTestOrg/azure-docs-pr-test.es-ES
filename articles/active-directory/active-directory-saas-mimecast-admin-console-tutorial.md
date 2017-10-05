---
title: "Tutorial: Integración de Azure Active Directory con Mimecast Admin Console | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Mimecast Admin Console."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="dd4a6-103">Tutorial: Integración de Azure Active Directory con Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="dd4a6-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="dd4a6-104">En este tutorial, obtendrá información sobre cómo integrar Mimecast Admin Console con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd4a6-105">La integración de Mimecast Admin Console con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dd4a6-106">En Azure AD puede controlar quién tiene acceso a Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="dd4a6-107">Puede permitir que los usuarios inicien sesión automáticamente en Mimecast Admin Console (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dd4a6-108">Puede administrar sus cuentas en una ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="dd4a6-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd4a6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dd4a6-110">Prerequisites</span></span>

<span data-ttu-id="dd4a6-111">Para configurar la integración de Azure AD con Mimecast Admin Console, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="dd4a6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4a6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd4a6-113">Un suscripción habilitada para inicio de sesión único en Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="dd4a6-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd4a6-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd4a6-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd4a6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd4a6-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd4a6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="dd4a6-118">Scenario description</span></span>
<span data-ttu-id="dd4a6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd4a6-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd4a6-121">Incorporación de Mimecast Admin Console desde la galería</span><span class="sxs-lookup"><span data-stu-id="dd4a6-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="dd4a6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4a6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="dd4a6-123">Incorporación de Mimecast Admin Console desde la galería</span><span class="sxs-lookup"><span data-stu-id="dd4a6-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="dd4a6-124">Para configurar la integración de Mimecast Admin Console en Azure AD, deberá agregar esta solución desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dd4a6-125">**Para agregar Mimecast Admin Console desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dd4a6-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dd4a6-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="dd4a6-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dd4a6-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-129">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="dd4a6-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="dd4a6-133">En el cuadro de búsqueda, escriba **Mimecast Admin Console**, seleccione **Mimecast Admin Console** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Mimecast Admin Console en la lista de resultados](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dd4a6-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4a6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dd4a6-136">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Mimecast Admin Console con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dd4a6-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dd4a6-137">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Mimecast Admin Console para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="dd4a6-138">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="dd4a6-139">Para establecer la relación de vínculo, en Mimecast Admin Console, asigne el valor del **nombre de usuario** en Azure AD como el valor del **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dd4a6-140">Para configurar y probar el inicio de sesión único de Azure AD con Mimecast Admin Console, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dd4a6-141">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dd4a6-142">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd4a6-143">**[Creación de un usuario de prueba de Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)**: para tener un homólogo de Britta Simon en Mimecast Admin Console que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd4a6-144">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd4a6-145">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dd4a6-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4a6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dd4a6-147">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="dd4a6-148">**Para configurar el inicio de sesión único de Azure AD con Mimecast Admin Console, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="dd4a6-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="dd4a6-149">En la página de integración de la aplicación **Mimecast Admin Console** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="dd4a6-151">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="dd4a6-153">En la sección **Dominio y direcciones URL de Mimecast Admin Console**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="dd4a6-155">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="dd4a6-156">La dirección URL de inicio de sesión es específica de la región.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="dd4a6-157">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="dd4a6-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="dd4a6-159">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd4a6-161">En la sección **Configuración de Mimecast Admin Console**, haga clic en **Configurar Mimecast Admin Console** para abrir la ventana **Configurar el inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dd4a6-162">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y Dirección URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuración de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="dd4a6-164">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="dd4a6-165">Vaya a **Servicios\>Aplicación**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="dd4a6-166">![Servicios](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Servicios")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="dd4a6-167">Haga clic en **Authentication Profiles**(Perfiles de autenticación).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="dd4a6-168">![Authentication Profiles (Perfiles de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles (Perfiles de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="dd4a6-169">Haga clic en **New Authentication Profile**(Nuevo perfil de autenticación).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="dd4a6-170">![New Authentication Profiles (Nuevos perfiles de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Authentication Profiles (Nuevos perfiles de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="dd4a6-171">En la sección **Authentication Profile** (Perfil de autenticación), realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="dd4a6-172">![Authentication Profile (Perfil de autenticación)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile (Perfil de autenticación)")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="dd4a6-173">a.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-173">a.</span></span> <span data-ttu-id="dd4a6-174">En el cuadro de texto **Description** (Descripción), escriba un nombre para la configuración.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="dd4a6-175">b.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-175">b.</span></span> <span data-ttu-id="dd4a6-176">Seleccione **Enforce SAML Authentication for Mimecast Admin Console**(Aplicar la autenticación SAML a Mimecast Admin Console).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="dd4a6-177">c.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-177">c.</span></span> <span data-ttu-id="dd4a6-178">Como **Provider** (Proveedor), seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="dd4a6-179">d.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-179">d.</span></span> <span data-ttu-id="dd4a6-180">Pegue el valor del **identificador de entidad de SAML**, que ha copiado de Azure Portal, en el cuadro de texto de **dirección URL del emisor**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="dd4a6-181">e.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-181">e.</span></span> <span data-ttu-id="dd4a6-182">Pegue la **dirección URL del inicio de sesión único de SAML**, que ha copiado de Azure Portal, en el cuadro de texto de **dirección URL del inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="dd4a6-183">f.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-183">f.</span></span> <span data-ttu-id="dd4a6-184">Pegue la **dirección URL del inicio de sesión único de SAML**, que ha copiado de Azure Portal, en el cuadro de texto de **dirección URL del cierre de sesión**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="dd4a6-185">El valor de Dirección URL de inicio de sesión y el valor de Dirección URL de cierre de sesión para Mimecast Admin Console son los mismos.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="dd4a6-186">g.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-186">g.</span></span> <span data-ttu-id="dd4a6-187">Abra el certificado en base 64 que descargó de Azure Portal en el Bloc de notas, quite la primera línea ("*--*") y la última línea ("*--*"), copie el resto del contenido en el Portapapeles y, después, péguelo en el cuadro de texto **Identity Provider Certificate (metadata)** (Certificado de proveedor de identidades [metadatos]).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="dd4a6-188">h.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-188">h.</span></span> <span data-ttu-id="dd4a6-189">Seleccione **Permitir inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="dd4a6-190">i.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-190">i.</span></span> <span data-ttu-id="dd4a6-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dd4a6-192">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dd4a6-193">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dd4a6-194">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd4a6-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dd4a6-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4a6-195">Create an Azure AD test user</span></span>

<span data-ttu-id="dd4a6-196">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dd4a6-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="dd4a6-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="dd4a6-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dd4a6-199">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="dd4a6-201">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="dd4a6-203">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="dd4a6-205">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-205">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dd4a6-207">a.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-207">a.</span></span> <span data-ttu-id="dd4a6-208">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd4a6-209">b.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-209">b.</span></span> <span data-ttu-id="dd4a6-210">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="dd4a6-211">c.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-211">c.</span></span> <span data-ttu-id="dd4a6-212">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="dd4a6-213">d.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-213">d.</span></span> <span data-ttu-id="dd4a6-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="dd4a6-215">Creación de un usuario de prueba de Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="dd4a6-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="dd4a6-216">Para permitir que los usuarios de Azure AD inicien sesión en Mimecast Admin Console, deben aprovisionarse en Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="dd4a6-217">En el caso de Mimecast Admin Console, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="dd4a6-218">Deberá registrar un dominio para poder crear los usuarios.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="dd4a6-219">**Siga estos pasos para configurar el aprovisionamiento de usuario:**</span><span class="sxs-lookup"><span data-stu-id="dd4a6-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="dd4a6-220">Inicie sesión en **Mimecast Admin Console** como administrador.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="dd4a6-221">Vaya a **Directorios\> Interno**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="dd4a6-222">![Directories (Directorios)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories (Directorios)")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="dd4a6-223">Haga clic en **Register New Domain**(Registrar nuevo dominio).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="dd4a6-224">![Register New Domain (Registrar nuevo dominio)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain (Registrar nuevo dominio)")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="dd4a6-225">Una vez creado el nuevo dominio, haga clic en **New Address**(Nueva dirección).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="dd4a6-226">![New Address (Nueva dirección)](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address (Nueva dirección)")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="dd4a6-227">En el cuadro de diálogo Nueva dirección, realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dd4a6-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="dd4a6-228">![Guardar](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Guardar")</span><span class="sxs-lookup"><span data-stu-id="dd4a6-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="dd4a6-229">a.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-229">a.</span></span> <span data-ttu-id="dd4a6-230">Escriba los datos de una cuenta de Azure AD válida que desee aprovisionar en los cuadros de texto correspondientes: **Email Address** (Dirección de correo electrónico), **Global Name** (Nombre global), **Password** (Contraseña) y **Confirm Password** (Confirmar contraseña).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="dd4a6-231">b.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-231">b.</span></span> <span data-ttu-id="dd4a6-232">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="dd4a6-233">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Mimecast Admin Console ofrecida por Mimecast Admin Console para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dd4a6-234">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd4a6-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="dd4a6-235">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="dd4a6-237">**Para asignar a Britta Simon a Mimecast Admin Console, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="dd4a6-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="dd4a6-238">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="dd4a6-240">En la lista de aplicaciones, seleccione **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![Vínculo a Mimecast Admin Console en la lista de aplicaciones](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="dd4a6-242">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="dd4a6-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-244">Click **Add** button.</span></span> <span data-ttu-id="dd4a6-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="dd4a6-247">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dd4a6-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd4a6-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dd4a6-250">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="dd4a6-250">Test single sign-on</span></span>

<span data-ttu-id="dd4a6-251">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dd4a6-252">Al hacer clic en el icono de Mimecast Admin Console en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="dd4a6-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="dd4a6-253">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd4a6-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dd4a6-254">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="dd4a6-254">Additional resources</span></span>

* [<span data-ttu-id="dd4a6-255">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd4a6-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd4a6-256">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd4a6-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

