---
title: "Tutorial: Integración de Azure Active Directory con GaggleAMP | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: c591cf99aecc4153e378c42a530b80deeca63158
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="a1fa5-103">Tutorial: integración de Azure Active Directory con GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="a1fa5-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="a1fa5-104">En este tutorial, aprenderá a integrar GaggleAMP con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1fa5-104">In this tutorial, you learn how to integrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1fa5-105">Integrar GaggleAMP con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-105">Integrating GaggleAMP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a1fa5-106">Puede controlar en Azure AD quién tiene acceso a GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-106">You can control in Azure AD who has access to GaggleAMP</span></span>
- <span data-ttu-id="a1fa5-107">Puede permitir que los usuarios inicien sesión automáticamente en GaggleAMP (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-107">You can enable your users to automatically get signed-on to GaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1fa5-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a1fa5-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a1fa5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1fa5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a1fa5-110">Prerequisites</span></span>

<span data-ttu-id="a1fa5-111">Para configurar la integración de Azure AD con GaggleAMP, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-111">To configure Azure AD integration with GaggleAMP, you need the following items:</span></span>

- <span data-ttu-id="a1fa5-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1fa5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1fa5-113">Una suscripción habilitada para inicio de sesión único en GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="a1fa5-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1fa5-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1fa5-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1fa5-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1fa5-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1fa5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1fa5-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a1fa5-118">Scenario description</span></span>
<span data-ttu-id="a1fa5-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1fa5-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1fa5-121">Adición de GaggleAMP desde la Galería</span><span class="sxs-lookup"><span data-stu-id="a1fa5-121">Adding GaggleAMP from the gallery</span></span>
2. <span data-ttu-id="a1fa5-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1fa5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-the-gallery"></a><span data-ttu-id="a1fa5-123">Adición de GaggleAMP desde la Galería</span><span class="sxs-lookup"><span data-stu-id="a1fa5-123">Adding GaggleAMP from the gallery</span></span>
<span data-ttu-id="a1fa5-124">Para configurar la integración de GaggleAMP en Azure AD, deberá agregar GaggleAMP desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-124">To configure the integration of GaggleAMP into Azure AD, you need to add GaggleAMP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a1fa5-125">**Para agregar GaggleAMP desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a1fa5-125">**To add GaggleAMP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a1fa5-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1fa5-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a1fa5-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a1fa5-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a1fa5-133">En el cuadro de búsqueda, escriba **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-133">In the search box, type **GaggleAMP**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="a1fa5-135">En el panel de resultados, seleccione **GaggleAMP** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-135">In the results panel, select **GaggleAMP**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1fa5-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1fa5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1fa5-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con GaggleAMP con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a1fa5-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a1fa5-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de GaggleAMP para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GaggleAMP is to a user in Azure AD.</span></span> <span data-ttu-id="a1fa5-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-140">In other words, a link relationship between an Azure AD user and the related user in GaggleAMP needs to be established.</span></span>

<span data-ttu-id="a1fa5-141">Para establecer la relación de vínculo en GaggleAMP, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-141">In GaggleAMP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a1fa5-142">Para configurar y probar el inicio de sesión único de Azure AD con GaggleAMP, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-142">To configure and test Azure AD single sign-on with GaggleAMP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a1fa5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a1fa5-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1fa5-145">**[Creación de un usuario de prueba de GaggleAMP](#creating-a-gaggleamp-test-user)**: para tener un homólogo de Britta Simon en GaggleAMP que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - to have a counterpart of Britta Simon in GaggleAMP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1fa5-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1fa5-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1fa5-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1fa5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1fa5-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="a1fa5-150">**Para configurar el inicio de sesión único de Azure AD con GaggleAMP, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a1fa5-150">**To configure Azure AD single sign-on with GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="a1fa5-151">En Azure Portal, en la página de integración de la aplicación **GaggleAMP**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-151">In the Azure portal, on the **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a1fa5-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="a1fa5-155">En la sección de **Dominio y direcciones URL de GaggleAMP**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-155">On the **GaggleAMP Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="a1fa5-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.gaggleamp.com`.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1fa5-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-158">The value is not real.</span></span> <span data-ttu-id="a1fa5-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="a1fa5-160">Para obtener este valor, póngase en contacto con el [equipo de soporte técnico de clientes de GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="a1fa5-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) to get the value.</span></span> 
 
4. <span data-ttu-id="a1fa5-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="a1fa5-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a1fa5-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a1fa5-165">En la sección **Configuración de GaggleAMP**, haga clic en **Configurar GaggleAMP** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-165">On the **GaggleAMP Configuration** section, click **Configure GaggleAMP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a1fa5-166">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="a1fa5-168">En otra instancia del explorador, desplácese a la página SSO de SAML creada por el equipo de soporte de Gaggle (por ejemplo: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="a1fa5-168">In another browser instance, navigate to the SAML SSO page created for you by the Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="a1fa5-169">En la página **SAML SSO** (Inicio de sesión único de SAML), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-169">On your **SAML SSO** page, perform the following steps:</span></span>  
   
    ![Inicio de sesión único de GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="a1fa5-171">a.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-171">a.</span></span> <span data-ttu-id="a1fa5-172">En el cuadro de texto **Emisor de proveedor de identidades**, pegue el valor de **URL del emisor** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-172">In the **Identity Provider Issuer** textbox, paste the value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="a1fa5-173">b.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-173">b.</span></span> <span data-ttu-id="a1fa5-174">En el cuadro de texto **Dirección URL del inicio de sesión único del proveedor de identidades**, pegue el valor de **Dirección URL del servicio de inicio de sesión único** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-174">In the **Identity Provider Single Sign-On URL** textbox, paste the  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="a1fa5-175">c.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-175">c.</span></span> <span data-ttu-id="a1fa5-176">Haga clic en **Guardar**</span><span class="sxs-lookup"><span data-stu-id="a1fa5-176">Click **Save**</span></span>      

    <span data-ttu-id="a1fa5-177">d.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-177">d.</span></span> <span data-ttu-id="a1fa5-178">Envíe el certificado **Certificado (Base64)** al [equipo de soporte técnico de GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="a1fa5-178">Send the **Certificate (Base64)** certificate to your [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="a1fa5-179">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a1fa5-180">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a1fa5-181">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1fa5-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1fa5-182">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1fa5-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1fa5-183">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a1fa5-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a1fa5-185">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a1fa5-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a1fa5-186">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a1fa5-188">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1fa5-190">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1fa5-192">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a1fa5-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1fa5-194">a.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-194">a.</span></span> <span data-ttu-id="a1fa5-195">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1fa5-196">b.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-196">b.</span></span> <span data-ttu-id="a1fa5-197">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1fa5-198">c.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-198">c.</span></span> <span data-ttu-id="a1fa5-199">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a1fa5-200">d.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-200">d.</span></span> <span data-ttu-id="a1fa5-201">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="a1fa5-202">Creación de un usuario de prueba de GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="a1fa5-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="a1fa5-203">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-203">The objective of this section is to create a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="a1fa5-204">GaggleAMP admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a1fa5-205">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-205">There is no action item for you in this section.</span></span> <span data-ttu-id="a1fa5-206">Durante un intento de obtener acceso a GaggleAMP se crea un nuevo usuario, en caso de que no exista.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-206">A new user is created during an attempt to access GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a1fa5-207">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1fa5-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a1fa5-208">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GaggleAMP.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a1fa5-210">**Para asignar a Britta Simon a GaggleAMP, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a1fa5-210">**To assign Britta Simon to GaggleAMP, perform the following steps:**</span></span>

1. <span data-ttu-id="a1fa5-211">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a1fa5-213">En la lista de aplicaciones, seleccione **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-213">In the applications list, select **GaggleAMP**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="a1fa5-215">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a1fa5-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-217">Click **Add** button.</span></span> <span data-ttu-id="a1fa5-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a1fa5-220">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a1fa5-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1fa5-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1fa5-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a1fa5-223">Testing single sign-on</span></span>

<span data-ttu-id="a1fa5-224">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a1fa5-225">Al hacer clic en el icono de GaggleAMP en el panel de acceso, debería iniciar sesión automáticamente en su aplicación GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="a1fa5-225">When you click the GaggleAMP tile in the Access Panel, you should get automatically signed-on to your GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1fa5-226">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a1fa5-226">Additional resources</span></span>

* [<span data-ttu-id="a1fa5-227">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1fa5-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1fa5-228">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a1fa5-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

