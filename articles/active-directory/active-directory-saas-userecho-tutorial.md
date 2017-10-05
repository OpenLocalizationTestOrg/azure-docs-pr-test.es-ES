---
title: "Tutorial: Integración de Azure Active Directory con UserEcho | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y UserEcho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2d824d8d5eb8a25db128397b908a126bd87213ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="32a15-103">Tutorial: integración de Azure Active Directory con UserEcho</span><span class="sxs-lookup"><span data-stu-id="32a15-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="32a15-104">En este tutorial, aprenderá a integrar UserEcho con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32a15-104">In this tutorial, you learn how to integrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32a15-105">Integrar UserEcho con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="32a15-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32a15-106">Puede controlar en Azure AD quién tiene acceso a UserEcho.</span><span class="sxs-lookup"><span data-stu-id="32a15-106">You can control in Azure AD who has access to UserEcho</span></span>
- <span data-ttu-id="32a15-107">Puede permitir que los usuarios inicien sesión automáticamente en UserEcho (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a15-107">You can enable your users to automatically get signed-on to UserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32a15-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="32a15-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32a15-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32a15-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32a15-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="32a15-110">Prerequisites</span></span>

<span data-ttu-id="32a15-111">Para configurar la integración de Azure AD con UserEcho, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="32a15-111">To configure Azure AD integration with UserEcho, you need the following items:</span></span>

- <span data-ttu-id="32a15-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32a15-113">Una suscripción a UserEcho habilitada para inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="32a15-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32a15-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="32a15-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32a15-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="32a15-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32a15-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="32a15-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32a15-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32a15-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32a15-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="32a15-118">Scenario description</span></span>
<span data-ttu-id="32a15-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="32a15-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32a15-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="32a15-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32a15-121">Incorporación de UserEcho desde la galería</span><span class="sxs-lookup"><span data-stu-id="32a15-121">Adding UserEcho from the gallery</span></span>
2. <span data-ttu-id="32a15-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a15-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-the-gallery"></a><span data-ttu-id="32a15-123">Incorporación de UserEcho desde la galería</span><span class="sxs-lookup"><span data-stu-id="32a15-123">Adding UserEcho from the gallery</span></span>
<span data-ttu-id="32a15-124">Para configurar la integración de UserEcho en Azure AD, deberá agregar UserEcho desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="32a15-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32a15-125">**Para agregar UserEcho desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="32a15-125">**To add UserEcho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32a15-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32a15-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32a15-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="32a15-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32a15-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="32a15-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="32a15-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32a15-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="32a15-133">En el cuadro de búsqueda, escriba **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="32a15-133">In the search box, type **UserEcho**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="32a15-135">En el panel de resultados, seleccione **UserEcho** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="32a15-135">In the results panel, select **UserEcho**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32a15-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a15-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32a15-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con UserEcho con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32a15-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32a15-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo en UserEcho de un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a15-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UserEcho is to a user in Azure AD.</span></span> <span data-ttu-id="32a15-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de UserEcho.</span><span class="sxs-lookup"><span data-stu-id="32a15-140">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span></span>

<span data-ttu-id="32a15-141">Para establecer la relación de vínculo, en UserEcho, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="32a15-141">In UserEcho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32a15-142">Para configurar y probar el inicio de sesión único de Azure AD con UserEcho, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="32a15-142">To configure and test Azure AD single sign-on with UserEcho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32a15-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="32a15-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32a15-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a15-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32a15-145">**[Creación de un usuario de prueba de UserEcho](#creating-a-userecho-test-user)**: para tener un homólogo de Britta Simon en UserEcho que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a15-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32a15-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a15-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32a15-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="32a15-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32a15-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a15-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32a15-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación UserEcho.</span><span class="sxs-lookup"><span data-stu-id="32a15-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="32a15-150">**Para configurar el inicio de sesión único de Azure AD con UserEcho, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="32a15-150">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="32a15-151">En Azure Portal, en la página de integración de la aplicación **UserEcho**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="32a15-151">In the Azure portal, on the **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="32a15-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="32a15-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="32a15-155">En la sección **Dominio y direcciones URL de UserEcho**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="32a15-155">On the **UserEcho Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="32a15-157">a.</span><span class="sxs-lookup"><span data-stu-id="32a15-157">a.</span></span> <span data-ttu-id="32a15-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.userecho.com/`.</span><span class="sxs-lookup"><span data-stu-id="32a15-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="32a15-159">b.</span><span class="sxs-lookup"><span data-stu-id="32a15-159">b.</span></span> <span data-ttu-id="32a15-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="32a15-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32a15-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="32a15-161">These values are not real.</span></span> <span data-ttu-id="32a15-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="32a15-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32a15-163">Póngase en contacto con el [equipo de soporte técnico de UserEcho](https://feedback.userecho.com/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="32a15-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values.</span></span> 

4. <span data-ttu-id="32a15-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="32a15-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="32a15-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="32a15-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32a15-168">En la sección **Configuración de UserEcho**, haga clic en **Configurar UserEcho** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="32a15-168">On the **UserEcho Configuration** section, click **Configure UserEcho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="32a15-169">Copie las **direcciones URL del servicio de inicio de sesión único de SAML y de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="32a15-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="32a15-171">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de UserEcho como administrador.</span><span class="sxs-lookup"><span data-stu-id="32a15-171">In another browser window, sign on to your UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="32a15-172">En la barra de herramientas de la parte superior, haga clic en el nombre de usuario para expandir el menú y, después, haga clic en **Instalación**.</span><span class="sxs-lookup"><span data-stu-id="32a15-172">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="32a15-174">Haga clic en **Integraciones**.</span><span class="sxs-lookup"><span data-stu-id="32a15-174">Click **Integrations**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="32a15-176">Haga clic en **Sitio web** y, después, en **Inicio de sesión único (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="32a15-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="32a15-178">Siga estos pasos en la página **Inicio de sesión único (SAML)** :</span><span class="sxs-lookup"><span data-stu-id="32a15-178">On the **Single sign-on (SAML)** page, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="32a15-180">a.</span><span class="sxs-lookup"><span data-stu-id="32a15-180">a.</span></span> <span data-ttu-id="32a15-181">En **Habilitado para SAML**, seleccione **Sí**.</span><span class="sxs-lookup"><span data-stu-id="32a15-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="32a15-182">b.</span><span class="sxs-lookup"><span data-stu-id="32a15-182">b.</span></span> <span data-ttu-id="32a15-183">Pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal en el cuadro de texto **SAML SSO URL** (Dirección URL de inicio de sesión de SAML).</span><span class="sxs-lookup"><span data-stu-id="32a15-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="32a15-184">c.</span><span class="sxs-lookup"><span data-stu-id="32a15-184">c.</span></span> <span data-ttu-id="32a15-185">Pegue el valor de la **dirección URL de cierre de sesión** que copió de Azure Portal en el cuadro de texto **Remote logoout URL** (Dirección URL de cierre de sesión remoto).</span><span class="sxs-lookup"><span data-stu-id="32a15-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="32a15-186">d.</span><span class="sxs-lookup"><span data-stu-id="32a15-186">d.</span></span> <span data-ttu-id="32a15-187">Abra el certificado descargado en el Bloc de notas, copie el contenido y luego péguelo en el cuadro de texto **Certificado X.509** .</span><span class="sxs-lookup"><span data-stu-id="32a15-187">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="32a15-188">e.</span><span class="sxs-lookup"><span data-stu-id="32a15-188">e.</span></span> <span data-ttu-id="32a15-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="32a15-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="32a15-190">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="32a15-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32a15-191">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="32a15-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32a15-192">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32a15-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32a15-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a15-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="32a15-194">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32a15-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="32a15-196">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="32a15-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32a15-197">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32a15-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32a15-199">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="32a15-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32a15-201">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32a15-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32a15-203">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="32a15-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32a15-205">a.</span><span class="sxs-lookup"><span data-stu-id="32a15-205">a.</span></span> <span data-ttu-id="32a15-206">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32a15-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32a15-207">b.</span><span class="sxs-lookup"><span data-stu-id="32a15-207">b.</span></span> <span data-ttu-id="32a15-208">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a15-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32a15-209">c.</span><span class="sxs-lookup"><span data-stu-id="32a15-209">c.</span></span> <span data-ttu-id="32a15-210">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="32a15-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32a15-211">d.</span><span class="sxs-lookup"><span data-stu-id="32a15-211">d.</span></span> <span data-ttu-id="32a15-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="32a15-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="32a15-213">Creación de un usuario de prueba de UserEcho</span><span class="sxs-lookup"><span data-stu-id="32a15-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="32a15-214">El objetivo de esta sección es crear una usuaria de prueba llamada Britta Simon en UserEcho.</span><span class="sxs-lookup"><span data-stu-id="32a15-214">The objective of this section is to create a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="32a15-215">**Para crear una usuaria llamada Britta Simon en UserEcho, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="32a15-215">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="32a15-216">Inicie sesión en el sitio de compañía de UserEcho como administrador.</span><span class="sxs-lookup"><span data-stu-id="32a15-216">Sign-on to your UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="32a15-217">En la barra de herramientas de la parte superior, haga clic en el nombre de usuario para expandir el menú y, después, haga clic en **Instalación**.</span><span class="sxs-lookup"><span data-stu-id="32a15-217">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="32a15-219">Haga clic en **Usuarios** para expandir la sección **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="32a15-219">Click **Users**, to expand the **Users** section.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="32a15-221">Haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="32a15-221">Click **Users**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="32a15-223">Haga clic en **Invitar a un nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="32a15-223">Click **Invite a new user**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="32a15-225">En el cuadro de diálogo **Invitar a un nuevo usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="32a15-225">On the **Invite a new user** dialog, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="32a15-227">a.</span><span class="sxs-lookup"><span data-stu-id="32a15-227">a.</span></span> <span data-ttu-id="32a15-228">En el cuadro de texto **Nombre**, escriba el nombre de un usuario, por ejemplo, Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a15-228">In the **Name** textbox, type name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="32a15-229">b.</span><span class="sxs-lookup"><span data-stu-id="32a15-229">b.</span></span>  <span data-ttu-id="32a15-230">En el cuadro de texto **Correo electrónico**, escriba la dirección de correo electrónico de un usuario, por ejemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="32a15-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="32a15-231">c.</span><span class="sxs-lookup"><span data-stu-id="32a15-231">c.</span></span> <span data-ttu-id="32a15-232">Haga clic en **Invitar**.</span><span class="sxs-lookup"><span data-stu-id="32a15-232">Click **Invite**.</span></span>

<span data-ttu-id="32a15-233">Se envía una invitación a Britta que le permite empezar a usar UserEcho.</span><span class="sxs-lookup"><span data-stu-id="32a15-233">An invitation is sent to Britta, which enables her to start using UserEcho.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32a15-234">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a15-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32a15-235">En esta sección, concederá acceso a Britta Simon a UserEcho para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="32a15-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserEcho.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="32a15-237">**Para asignar a Britta Simon a UserEcho, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="32a15-237">**To assign Britta Simon to UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="32a15-238">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="32a15-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="32a15-240">En la lista de aplicaciones, seleccione **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="32a15-240">In the applications list, select **UserEcho**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="32a15-242">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="32a15-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="32a15-244">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="32a15-244">Click **Add** button.</span></span> <span data-ttu-id="32a15-245">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="32a15-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="32a15-247">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="32a15-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32a15-248">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="32a15-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32a15-249">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="32a15-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32a15-250">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="32a15-250">Testing single sign-on</span></span>

<span data-ttu-id="32a15-251">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="32a15-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="32a15-252">Al hacer clic en el icono de UserEcho en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación UserEcho.</span><span class="sxs-lookup"><span data-stu-id="32a15-252">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32a15-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="32a15-253">Additional resources</span></span>

* [<span data-ttu-id="32a15-254">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32a15-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32a15-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32a15-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

