---
title: "Tutorial: integración de Azure Active Directory con StatusPage | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y StatusPage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: fa16cdec7b89404c140435fe57d5aa4b08cfa985
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="791ab-103">Tutorial: Integración de Azure Active Directory con StatusPage</span><span class="sxs-lookup"><span data-stu-id="791ab-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="791ab-104">En este tutorial, obtendrá información sobre cómo integrar StatusPage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="791ab-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="791ab-105">La integración de StatusPage con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="791ab-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="791ab-106">Puede controlar en Azure AD quién tiene acceso a StatusPage.</span><span class="sxs-lookup"><span data-stu-id="791ab-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="791ab-107">Puede permitir que los usuarios inicien sesión automáticamente en StatusPage (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="791ab-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="791ab-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="791ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="791ab-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="791ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="791ab-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="791ab-110">Prerequisites</span></span>

<span data-ttu-id="791ab-111">Para configurar la integración de Azure AD con StatusPage, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="791ab-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="791ab-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="791ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="791ab-113">Una suscripción habilitada para inicio de sesión único en StatusPage</span><span class="sxs-lookup"><span data-stu-id="791ab-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="791ab-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="791ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="791ab-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="791ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="791ab-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="791ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="791ab-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="791ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="791ab-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="791ab-118">Scenario description</span></span>
<span data-ttu-id="791ab-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="791ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="791ab-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="791ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="791ab-121">Incorporación de StatusPage desde la galería</span><span class="sxs-lookup"><span data-stu-id="791ab-121">Adding StatusPage from the gallery</span></span>
2. <span data-ttu-id="791ab-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="791ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="791ab-123">Incorporación de StatusPage desde la galería</span><span class="sxs-lookup"><span data-stu-id="791ab-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="791ab-124">Para configurar la integración de StatusPage en Azure AD, deberá agregar StatusPage desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="791ab-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="791ab-125">**Para agregar StatusPage desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="791ab-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="791ab-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="791ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="791ab-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="791ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="791ab-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="791ab-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="791ab-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="791ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="791ab-133">En el cuadro de búsqueda, escriba **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="791ab-133">In the search box, type **StatusPage**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. <span data-ttu-id="791ab-135">En el panel de resultados, seleccione **StatusPage** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="791ab-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="791ab-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="791ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="791ab-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con StatusPage con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="791ab-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="791ab-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de StatusPage para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="791ab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="791ab-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de StatusPage.</span><span class="sxs-lookup"><span data-stu-id="791ab-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="791ab-141">Para establecer la relación de vínculo, en StatusPage, asigne el valor del **nombre de usuario** en Azure AD como valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="791ab-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="791ab-142">Para configurar y probar el inicio de sesión único de Azure AD con StatusPage, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="791ab-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="791ab-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="791ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="791ab-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="791ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="791ab-145">**[Creación de un usuario de prueba de StatusPage](#creating-a-statuspage-test-user)**: para tener un homólogo de Britta Simon en StatusPage que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="791ab-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="791ab-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="791ab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="791ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="791ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="791ab-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="791ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="791ab-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación StatusPage.</span><span class="sxs-lookup"><span data-stu-id="791ab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="791ab-150">**Para configurar el inicio de sesión único de Azure AD con StatusPage, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="791ab-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="791ab-151">En Azure Portal, en la página de integración de la aplicación **StatusPage**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="791ab-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="791ab-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="791ab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. <span data-ttu-id="791ab-155">En la sección **Dominio y direcciones URL de StatusPage**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="791ab-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="791ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="791ab-157">a.</span></span> <span data-ttu-id="791ab-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="791ab-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="791ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="791ab-159">b.</span></span> <span data-ttu-id="791ab-160">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="791ab-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="791ab-161">Póngase en contacto con el equipo de soporte técnico de StatusPage [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)a fin de solicitar los metadatos necesarios para configurar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="791ab-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="791ab-162">a.</span><span class="sxs-lookup"><span data-stu-id="791ab-162">a.</span></span> <span data-ttu-id="791ab-163">En los metadatos, copie el valor de Emisor y luego péguelo en el cuadro de texto **Identificador** .</span><span class="sxs-lookup"><span data-stu-id="791ab-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="791ab-164">b.</span><span class="sxs-lookup"><span data-stu-id="791ab-164">b.</span></span> <span data-ttu-id="791ab-165">En los metadatos, copie el valor de URL de respuesta y luego péguelo en el cuadro de texto **URL de respuesta** .</span><span class="sxs-lookup"><span data-stu-id="791ab-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

4. <span data-ttu-id="791ab-166">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="791ab-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. <span data-ttu-id="791ab-168">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="791ab-168">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="791ab-170">En la sección **Configuración de StatusPage**, haga clic en **Configurar StatusPage** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="791ab-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="791ab-171">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="791ab-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. <span data-ttu-id="791ab-173">En otra ventana del explorador, inicie sesión en su sitio de la empresa de StatusPage como administrador.</span><span class="sxs-lookup"><span data-stu-id="791ab-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

8. <span data-ttu-id="791ab-174">En la barra de herramientas principal, haga clic en **Administrar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="791ab-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. <span data-ttu-id="791ab-176">Haga clic en la pestaña **Inicio de sesión único** .</span><span class="sxs-lookup"><span data-stu-id="791ab-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. <span data-ttu-id="791ab-178">En la página Configuración de SSO, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="791ab-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="791ab-181">a.</span><span class="sxs-lookup"><span data-stu-id="791ab-181">a.</span></span> <span data-ttu-id="791ab-182">En el cuadro de texto **SSO Target URL** (Dirección URL de destino de SSO), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="791ab-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="791ab-183">b.</span><span class="sxs-lookup"><span data-stu-id="791ab-183">b.</span></span> <span data-ttu-id="791ab-184">Abra el certificado descargado en el Bloc de notas, copie el contenido y luego péguelo en el cuadro de texto **Certificado** .</span><span class="sxs-lookup"><span data-stu-id="791ab-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="791ab-185">c.</span><span class="sxs-lookup"><span data-stu-id="791ab-185">c.</span></span> <span data-ttu-id="791ab-186">Haga clic en **GUARDAR CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="791ab-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="791ab-187">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="791ab-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="791ab-188">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="791ab-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="791ab-189">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="791ab-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="791ab-190">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="791ab-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="791ab-191">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="791ab-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="791ab-193">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="791ab-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="791ab-194">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="791ab-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="791ab-196">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="791ab-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="791ab-198">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="791ab-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="791ab-200">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="791ab-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="791ab-202">a.</span><span class="sxs-lookup"><span data-stu-id="791ab-202">a.</span></span> <span data-ttu-id="791ab-203">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="791ab-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="791ab-204">b.</span><span class="sxs-lookup"><span data-stu-id="791ab-204">b.</span></span> <span data-ttu-id="791ab-205">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="791ab-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="791ab-206">c.</span><span class="sxs-lookup"><span data-stu-id="791ab-206">c.</span></span> <span data-ttu-id="791ab-207">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="791ab-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="791ab-208">d.</span><span class="sxs-lookup"><span data-stu-id="791ab-208">d.</span></span> <span data-ttu-id="791ab-209">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="791ab-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="791ab-210">Creación de un usuario de prueba de StatusPage</span><span class="sxs-lookup"><span data-stu-id="791ab-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="791ab-211">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en StatusPage.</span><span class="sxs-lookup"><span data-stu-id="791ab-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="791ab-212">StatusPage admite el aprovisionamiento Just-In-Time.</span><span class="sxs-lookup"><span data-stu-id="791ab-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="791ab-213">Ya lo ha habilitado en [Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="791ab-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="791ab-214">**Para crear un usuario llamado Britta Simon en StatusPage, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="791ab-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="791ab-215">Inicie sesión en su sitio de la empresa StatusPage como administrador.</span><span class="sxs-lookup"><span data-stu-id="791ab-215">Sign-on to your StatusPage company site as an administrator.</span></span>

2. <span data-ttu-id="791ab-216">En el menú de la parte superior, haga clic en **Administrar cuenta**.</span><span class="sxs-lookup"><span data-stu-id="791ab-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. <span data-ttu-id="791ab-218">Haga clic en la pestaña **Team Members** (Miembros del equipo).</span><span class="sxs-lookup"><span data-stu-id="791ab-218">Click the **Team Members** tab.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. <span data-ttu-id="791ab-220">Haga clic en **ADD TEAM MEMBER**(Agregar miembro del equipo).</span><span class="sxs-lookup"><span data-stu-id="791ab-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. <span data-ttu-id="791ab-222">Escriba **Email Address** (Dirección de correo electrónico), **First Name** (Nombre) y **Surname** (Apellido) en los cuadros de texto correspondientes para un usuario válido que quiera aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="791ab-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. <span data-ttu-id="791ab-224">En **Rol**, elija **Administrador de clientes**.</span><span class="sxs-lookup"><span data-stu-id="791ab-224">As **Role**, choose **Client Administrator**.</span></span>

7. <span data-ttu-id="791ab-225">Haga clic en **CREATE ACCOUNT** (CREAR CUENTA).</span><span class="sxs-lookup"><span data-stu-id="791ab-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="791ab-226">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="791ab-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="791ab-227">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a StatusPage.</span><span class="sxs-lookup"><span data-stu-id="791ab-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="791ab-229">**Para asignar a Britta Simon a StatusPage, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="791ab-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="791ab-230">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="791ab-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="791ab-232">En la lista de aplicaciones, seleccione **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="791ab-232">In the applications list, select **StatusPage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. <span data-ttu-id="791ab-234">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="791ab-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="791ab-236">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="791ab-236">Click **Add** button.</span></span> <span data-ttu-id="791ab-237">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="791ab-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="791ab-239">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="791ab-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="791ab-240">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="791ab-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="791ab-241">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="791ab-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="791ab-242">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="791ab-242">Testing single sign-on</span></span>

<span data-ttu-id="791ab-243">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="791ab-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="791ab-244">Al hacer clic en el icono de StatusPage en el panel de acceso, debería iniciar sesión automáticamente en su aplicación StatusPage.</span><span class="sxs-lookup"><span data-stu-id="791ab-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="791ab-245">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="791ab-245">Additional resources</span></span>

* [<span data-ttu-id="791ab-246">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="791ab-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="791ab-247">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="791ab-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png
