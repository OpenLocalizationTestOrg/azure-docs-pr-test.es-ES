---
title: "Tutorial: Integración de Azure Active Directory con Autotask Workplace | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Autotask Workplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 45130162271b20860607497ff93c6a668c415233
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="81422-103">Tutorial: Integración de Azure Active Directory con Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="81422-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="81422-104">En este tutorial, obtendrá información sobre cómo integrar Autotask Workplace con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81422-104">In this tutorial, you learn how to integrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81422-105">La integración de Autotask Workplace con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="81422-105">Integrating Autotask Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81422-106">En Azure AD puede controlar quién tiene acceso a Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="81422-106">You can control in Azure AD who has access to Autotask Workplace</span></span>
- <span data-ttu-id="81422-107">Puede permitir que los usuarios inicien sesión automáticamente en Autotask Workplace (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81422-107">You can enable your users to automatically get signed-on to Autotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81422-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="81422-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81422-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81422-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81422-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="81422-110">Prerequisites</span></span>

<span data-ttu-id="81422-111">Para configurar la integración de Azure AD con Autotask Workplace, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="81422-111">To configure Azure AD integration with Autotask Workplace, you need the following items:</span></span>

- <span data-ttu-id="81422-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81422-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81422-113">Una suscripción habilitada para inicio de sesión único en Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="81422-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="81422-114">Es necesario que sea administrador o superadministrador en Workplace.</span><span class="sxs-lookup"><span data-stu-id="81422-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="81422-115">Tiene que tener una cuenta de administrador en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81422-115">You must have an administrator account in the Azure AD.</span></span>
- <span data-ttu-id="81422-116">Los usuarios que vayan a usar esta característica tienen que tener cuentas en Workplace y Azure AD y las direcciones de correo electrónico para ambas cuentas tienen que coincidir.</span><span class="sxs-lookup"><span data-stu-id="81422-116">The users that will utilize this feature must have accounts within Workplace and the Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="81422-117">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="81422-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81422-118">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="81422-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81422-119">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="81422-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81422-120">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81422-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81422-121">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="81422-121">Scenario description</span></span>
<span data-ttu-id="81422-122">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="81422-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81422-123">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="81422-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81422-124">Incorporación de Autotask Workplace desde la galería</span><span class="sxs-lookup"><span data-stu-id="81422-124">Adding Autotask Workplace from the gallery</span></span>
2. <span data-ttu-id="81422-125">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81422-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-the-gallery"></a><span data-ttu-id="81422-126">Incorporación de Autotask Workplace desde la galería</span><span class="sxs-lookup"><span data-stu-id="81422-126">Adding Autotask Workplace from the gallery</span></span>
<span data-ttu-id="81422-127">Para configurar la integración de Autotask Workplace en Azure AD, deberá agregar Autotask Workplace desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="81422-127">To configure the integration of Autotask Workplace into Azure AD, you need to add Autotask Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81422-128">**Para agregar Autotask Workplace desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="81422-128">**To add Autotask Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81422-129">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81422-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Botón Azure Active Directory][1]

2. <span data-ttu-id="81422-131">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="81422-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81422-132">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81422-132">Then go to **All applications**.</span></span>

    ![Hoja Aplicaciones empresariales][2]
    
3. <span data-ttu-id="81422-134">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81422-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Botón Nueva aplicación][3]

4. <span data-ttu-id="81422-136">En el cuadro de búsqueda, escriba **Autotask Workplace**, seleccione **Autotask Workplace** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81422-136">In the search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button to add the application.</span></span>

    ![Autotask Workplace en la lista de resultados](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="81422-138">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="81422-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="81422-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Autotask Workplace con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81422-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="81422-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Autotask Workplace para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81422-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Autotask Workplace is to a user in Azure AD.</span></span> <span data-ttu-id="81422-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="81422-141">In other words, a link relationship between an Azure AD user and the related user in Autotask Workplace needs to be established.</span></span>

<span data-ttu-id="81422-142">Para establecer la relación de vínculo, en Autotask Workplace, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="81422-142">In Autotask Workplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81422-143">Para configurar y probar el inicio de sesión único de Azure AD con Autotask Workplace, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="81422-143">To configure and test Azure AD single sign-on with Autotask Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81422-144">**[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para permitir que los usuarios utilicen esta característica.</span><span class="sxs-lookup"><span data-stu-id="81422-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81422-145">**[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81422-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81422-146">**[Creación de un usuario de prueba de Autotask Workplace](#create-an-autotask-workplace-test-user)**: para tener un homólogo de Britta Simon en Autotask Workplace que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81422-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - to have a counterpart of Britta Simon in Autotask Workplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81422-147">**[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81422-147">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81422-148">**[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="81422-148">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="81422-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81422-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="81422-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="81422-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="81422-151">**Para configurar el inicio de sesión único de Azure AD con Autotask Workplace, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="81422-151">**To configure Azure AD single sign-on with Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="81422-152">En la página de integración de la aplicación **Autotask Workplace** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="81422-152">In the Azure portal, on the **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="81422-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="81422-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="81422-156">Si desea configurar la aplicación en el modo iniciado por **IDP** , realice los pasos siguientes en la sección **Dominio y direcciones URL de Autotask Workplace**:</span><span class="sxs-lookup"><span data-stu-id="81422-156">If you wish to configure the application in **IDP** initiated mode, perform the following steps on the **Autotask Workplace Domain and URLs** section:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Autotask Workplace para IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="81422-158">a.</span><span class="sxs-lookup"><span data-stu-id="81422-158">a.</span></span> <span data-ttu-id="81422-159">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="81422-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="81422-160">b.</span><span class="sxs-lookup"><span data-stu-id="81422-160">b.</span></span> <span data-ttu-id="81422-161">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="81422-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="81422-162">Si desea configurar la aplicación en modo iniciado por **SP**, active **Mostrar configuración avanzada de URL** y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81422-162">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Autotask Workplace para SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="81422-164">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.awp.autotask.net/loginsso`.</span><span class="sxs-lookup"><span data-stu-id="81422-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="81422-165">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="81422-165">These values are not real.</span></span> <span data-ttu-id="81422-166">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="81422-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="81422-167">Póngase en contacto con el [equipo de soporte de cliente de Autotask Workplace](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="81422-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get these values.</span></span> 

5. <span data-ttu-id="81422-168">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="81422-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Vínculo de descarga del certificado](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="81422-170">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="81422-170">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="81422-172">En una ventana del explorador web diferente, inicie sesión en Workplace en línea con las credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="81422-172">In a different web browser window, Log in to Workplace Online using the administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="81422-173">Al configurar la extensión IdP tendrá que especificar un subdominio.</span><span class="sxs-lookup"><span data-stu-id="81422-173">When configuring the IdP, a subdomain will need to be specified.</span></span> <span data-ttu-id="81422-174">Para confirmar el subdominio correcto, inicie sesión en Workplace en línea.</span><span class="sxs-lookup"><span data-stu-id="81422-174">To confirm the correct subdomain, login to Workplace Online.</span></span> <span data-ttu-id="81422-175">Una vez iniciada la sesión, anote el subdominio en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="81422-175">Once logged in, make note to the subdomain in the URL.</span></span>
    ><span data-ttu-id="81422-176">El subdominio es la parte entre "https://" y ".awp.autotask.net/" y debe ser us, eu, ca, o au.</span><span class="sxs-lookup"><span data-stu-id="81422-176">The subdomain is the part between the “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="81422-177">Vaya a **Configuration**(Configuración) > **Single Sign-On** (Inicio de sesión único) y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81422-177">Go to **Configuration** > **Single Sign-On** and perform the following steps:</span></span>

    ![Configuración de inicio de sesión único de Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="81422-179">a.</span><span class="sxs-lookup"><span data-stu-id="81422-179">a.</span></span> <span data-ttu-id="81422-180">Seleccione la opción **XML Metadata File** (Archivo de metadatos XML) y, a continuación, cargue los **metadatos XML** descargados de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="81422-180">Select the **XML Metadata File** option, and then upload the **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="81422-181">b.</span><span class="sxs-lookup"><span data-stu-id="81422-181">b.</span></span> <span data-ttu-id="81422-182">Haga clic en **Enable SSO** (Habilitar SSO).</span><span class="sxs-lookup"><span data-stu-id="81422-182">Click **Enable SSO**.</span></span>
    
    ![Aprobación de configuración de inicio de sesión único de Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="81422-184">c.</span><span class="sxs-lookup"><span data-stu-id="81422-184">c.</span></span> <span data-ttu-id="81422-185">Seleccione la casilla **I confirm this information is correct and I trust this IdP** (Confirmo que esta información es correcta y que confío en este IdP).</span><span class="sxs-lookup"><span data-stu-id="81422-185">Select the **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="81422-186">d.</span><span class="sxs-lookup"><span data-stu-id="81422-186">d.</span></span> <span data-ttu-id="81422-187">Haga clic en **Approve** (Aprobar).</span><span class="sxs-lookup"><span data-stu-id="81422-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="81422-188">Si necesita ayuda con la configuración de Autotask Workplace, consulte [esta página](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) para obtener asistencia con la cuenta de Workplace.</span><span class="sxs-lookup"><span data-stu-id="81422-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to get assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="81422-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="81422-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81422-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="81422-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81422-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81422-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="81422-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81422-192">Create an Azure AD test user</span></span>

<span data-ttu-id="81422-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81422-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="81422-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="81422-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81422-196">En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="81422-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Botón Azure Active Directory](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="81422-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="81422-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="81422-200">En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="81422-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Botón Agregar](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="81422-202">En el cuadro de diálogo **Usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="81422-202">In the **User** dialog box, perform the following steps:</span></span>

    ![Cuadro de diálogo Usuario](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="81422-204">a.</span><span class="sxs-lookup"><span data-stu-id="81422-204">a.</span></span> <span data-ttu-id="81422-205">En el cuadro **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81422-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81422-206">b.</span><span class="sxs-lookup"><span data-stu-id="81422-206">b.</span></span> <span data-ttu-id="81422-207">En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81422-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="81422-208">c.</span><span class="sxs-lookup"><span data-stu-id="81422-208">c.</span></span> <span data-ttu-id="81422-209">Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="81422-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="81422-210">d.</span><span class="sxs-lookup"><span data-stu-id="81422-210">d.</span></span> <span data-ttu-id="81422-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="81422-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="81422-212">Creación de un usuario de prueba de Autotask Workplace</span><span class="sxs-lookup"><span data-stu-id="81422-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="81422-213">En esta sección, creará un usuario llamado Britta Simon en Autotask.</span><span class="sxs-lookup"><span data-stu-id="81422-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="81422-214">Colabore con el [equipo de soporte técnico de Autotask Workplace](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) para agregar los usuarios en esta plataforma.</span><span class="sxs-lookup"><span data-stu-id="81422-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) to add the users in the Autotask Workplace platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="81422-215">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="81422-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="81422-216">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="81422-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Autotask Workplace.</span></span>

![Asignación del rol de usuario][200] 

<span data-ttu-id="81422-218">**Para asignar la usuaria Britta Simon a Autotask Workplace, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="81422-218">**To assign Britta Simon to Autotask Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="81422-219">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="81422-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="81422-221">En la lista de aplicaciones, seleccione **Autotask Workplace**.</span><span class="sxs-lookup"><span data-stu-id="81422-221">In the applications list, select **Autotask Workplace**.</span></span>

    ![Vínculo de Autotask Workplace en la lista de aplicaciones](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="81422-223">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81422-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Vínculo "Usuarios y grupos"][202]

4. <span data-ttu-id="81422-225">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="81422-225">Click **Add** button.</span></span> <span data-ttu-id="81422-226">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81422-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Panel Agregar asignación][203]

5. <span data-ttu-id="81422-228">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="81422-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81422-229">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="81422-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81422-230">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="81422-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="81422-231">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="81422-231">Test single sign-on</span></span>

<span data-ttu-id="81422-232">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="81422-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81422-233">Al hacer clic en el icono de Autotask Workplace en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación de Autotask Workplace.</span><span class="sxs-lookup"><span data-stu-id="81422-233">When you click the Autotask Workplace tile in the Access Panel, you should get automatically signed-on to your Autotask Workplace application.</span></span>
<span data-ttu-id="81422-234">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81422-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81422-235">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="81422-235">Additional resources</span></span>

* [<span data-ttu-id="81422-236">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81422-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81422-237">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81422-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

