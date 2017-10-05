---
title: "Tutorial: Integración de Azure Active Directory con Lifesize Cloud | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Lifesize Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7542360f9c75786bf400553090ba0a891d9c2fcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="c38e2-103">Tutorial: Integración de Azure Active Directory con Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="c38e2-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="c38e2-104">En este tutorial, aprenderá a integrar Lifesize Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c38e2-104">In this tutorial, you learn how to integrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c38e2-105">La integración de Lifesize Cloud con Azure AD ofrece las ventajas siguientes:</span><span class="sxs-lookup"><span data-stu-id="c38e2-105">Integrating Lifesize Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c38e2-106">En Azure AD se puede controlar quién tiene acceso a Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="c38e2-106">You can control in Azure AD who has access to Lifesize Cloud</span></span>
- <span data-ttu-id="c38e2-107">Puede permitir que los usuarios inicien sesión automáticamente en Lifesize Cloud (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c38e2-107">You can enable your users to automatically get signed-on to Lifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c38e2-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c38e2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c38e2-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c38e2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c38e2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c38e2-110">Prerequisites</span></span>

<span data-ttu-id="c38e2-111">Para configurar la integración de Azure AD con Lifesize Cloud se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="c38e2-111">To configure Azure AD integration with Lifesize Cloud, you need the following items:</span></span>

- <span data-ttu-id="c38e2-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c38e2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c38e2-113">Una suscripción habilitada para el inicio de sesión único en Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="c38e2-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c38e2-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="c38e2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c38e2-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="c38e2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c38e2-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c38e2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c38e2-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c38e2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c38e2-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="c38e2-118">Scenario description</span></span>
<span data-ttu-id="c38e2-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="c38e2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c38e2-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="c38e2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c38e2-121">Agregar Lifesize Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="c38e2-121">Adding Lifesize Cloud from the gallery</span></span>
2. <span data-ttu-id="c38e2-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c38e2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-the-gallery"></a><span data-ttu-id="c38e2-123">Agregar Lifesize Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="c38e2-123">Adding Lifesize Cloud from the gallery</span></span>
<span data-ttu-id="c38e2-124">Para configurar la integración de Lifesize Cloud en Azure AD, necesita agregar Lifesize Cloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="c38e2-124">To configure the integration of Lifesize Cloud into Azure AD, you need to add Lifesize Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c38e2-125">**Para agregar Lifesize Cloud desde la galería, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="c38e2-125">**To add Lifesize Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c38e2-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c38e2-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c38e2-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="c38e2-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c38e2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="c38e2-133">En el cuadro de búsqueda, escriba **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-133">In the search box, type **Lifesize Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="c38e2-135">En el panel de resultados, seleccione **Lifesize Cloud** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c38e2-135">In the results panel, select **Lifesize Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c38e2-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c38e2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c38e2-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Lifesize Cloud con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c38e2-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c38e2-139">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Lifesize Cloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c38e2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lifesize Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="c38e2-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="c38e2-140">In other words, a link relationship between an Azure AD user and the related user in Lifesize Cloud needs to be established.</span></span>

<span data-ttu-id="c38e2-141">Para establecer la relación de vínculo, en Lifesize Cloud, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-141">In Lifesize Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c38e2-142">Para configurar y probar el inicio de sesión único de Azure AD con Lifesize Cloud, es necesario completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="c38e2-142">To configure and test Azure AD single sign-on with Lifesize Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c38e2-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="c38e2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c38e2-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c38e2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c38e2-145">**[Creación de un usuario de prueba de Lifesize Cloud](#creating-a-lifesize-cloud-test-user)**: el objetivo es tener un homólogo de Britta Simon en Lifesize Cloud que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c38e2-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - to have a counterpart of Britta Simon in Lifesize Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c38e2-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c38e2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c38e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="c38e2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c38e2-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c38e2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c38e2-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="c38e2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="c38e2-150">**Para configurar el inicio de sesión único de Azure AD con Lifesize Cloud, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="c38e2-150">**To configure Azure AD single sign-on with Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="c38e2-151">En la página de integración de la aplicación **Lifesize Cloud** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-151">In the Azure portal, on the **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="c38e2-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="c38e2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="c38e2-155">En la sección **Dominio y direcciones URL de Lifesize Cloud**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c38e2-155">On the **Lifesize Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="c38e2-157">a.</span><span class="sxs-lookup"><span data-stu-id="c38e2-157">a.</span></span> <span data-ttu-id="c38e2-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://login.lifesizecloud.com/ls/?acs`.</span><span class="sxs-lookup"><span data-stu-id="c38e2-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="c38e2-159">b.</span><span class="sxs-lookup"><span data-stu-id="c38e2-159">b.</span></span> <span data-ttu-id="c38e2-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c38e2-160">In the **Identifier** textbox, type a URL using the following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="c38e2-161">Active la casilla **Mostrar configuración avanzada de URL** y realice el siguiente paso:</span><span class="sxs-lookup"><span data-stu-id="c38e2-161">Check **Show advanced URL settings**, perform the following step:</span></span>    
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="c38e2-163">En el cuadro de texto **Estado de la retransmisión**, escriba una dirección URL que siga este patrón:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="c38e2-163">In the **Relay state** textbox, type a URL using the following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="c38e2-164">Tenga en cuenta que estos no son valores reales.</span><span class="sxs-lookup"><span data-stu-id="c38e2-164">Please note that these are not the real values.</span></span> <span data-ttu-id="c38e2-165">Deberá actualizar estos valores con la dirección URL de inicio de sesión, el estado de la retransmisión y el identificador reales.</span><span class="sxs-lookup"><span data-stu-id="c38e2-165">you have to update these values with the actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="c38e2-166">Póngase en contacto con el [equipo de soporte técnico de Lifesize Cloud Client](https://www.lifesize.com/support) para obtener los valores de dirección URL de inicio de sesión e identificador; el valor de estado de retransmisión lo puede obtener de la configuración del inicio de sesión único que se explica más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c38e2-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) to get Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in the tutorial.</span></span>

4. <span data-ttu-id="c38e2-167">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="c38e2-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="c38e2-169">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="c38e2-169">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c38e2-171">En la sección **Configuración de Lifesize Cloud**, haga clic en **Configurar Lifesize Cloud** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-171">On the **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c38e2-172">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-172">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="c38e2-174">Para configurar SSO para su aplicación, inicie sesión en la aplicación de Lifesize Cloud con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="c38e2-174">To get SSO configured for your application, login into the Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="c38e2-175">En la esquina superior derecha, haga clic en su nombre y, después, en **Configuración avanzada**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-175">In the top right corner click on your name and then click on the **Advance Settings**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="c38e2-177">En Configuración avanzada, haga clic en el vínculo **Configuración de SSO**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-177">In the Advance Settings now click on the **SSO Configuration** link.</span></span> <span data-ttu-id="c38e2-178">Se abrirá la página de configuración de SSO de la instancia.</span><span class="sxs-lookup"><span data-stu-id="c38e2-178">It will open the SSO Configuration page for your instance.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="c38e2-180">Ahora, configure los valores siguientes en la interfaz de configuración de SSO.</span><span class="sxs-lookup"><span data-stu-id="c38e2-180">Now configure the following values in the SSO configuration UI.</span></span>    
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="c38e2-182">a.</span><span class="sxs-lookup"><span data-stu-id="c38e2-182">a.</span></span> <span data-ttu-id="c38e2-183">En el cuadro de texto **Emisor de proveedor de identidades**, pegue el valor de **id. de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c38e2-183">In **Identity Provider Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c38e2-184">b.</span><span class="sxs-lookup"><span data-stu-id="c38e2-184">b.</span></span>  <span data-ttu-id="c38e2-185">En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c38e2-185">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c38e2-186">c.</span><span class="sxs-lookup"><span data-stu-id="c38e2-186">c.</span></span> <span data-ttu-id="c38e2-187">Abra el certificado codificado en base 64 descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado X.509**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="c38e2-188">d.</span><span class="sxs-lookup"><span data-stu-id="c38e2-188">d.</span></span> <span data-ttu-id="c38e2-189">En la asignación de atributos de SAML, en el cuadro de texto Nombre, escriba el valor **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-189">In the SAML Attribute mappings for the First Name text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="c38e2-190">e.</span><span class="sxs-lookup"><span data-stu-id="c38e2-190">e.</span></span> <span data-ttu-id="c38e2-191">En la asignación de atributos de SAML, en el cuadro de texto **Apellidos**, escriba el valor **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-191">In the SAML Attribute mapping for the **Last Name** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="c38e2-192">f.</span><span class="sxs-lookup"><span data-stu-id="c38e2-192">f.</span></span> <span data-ttu-id="c38e2-193">En la asignación de atributos de SAML, en el cuadro de texto **Correo electrónico**, escriba el valor **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-193">In the SAML Attribute mapping for the **Email** text box enter the value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="c38e2-194">Para comprobar la configuración, puede hacer clic en el botón **Probar**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-194">To check the configuration you can click on the **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c38e2-195">Para realizar una prueba correctamente, necesita completar el asistente para configuración en Azure AD y, además, proporcionar acceso los usuarios o grupos que pueden realizar la prueba.</span><span class="sxs-lookup"><span data-stu-id="c38e2-195">For successful testing you need to complete the configuration wizard in Azure AD and also provide access to users or groups who can perform the test.</span></span>

12. <span data-ttu-id="c38e2-196">Para habilitar SSO, seleccione el botón **Habilitar SSO**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-196">Enable the SSO by checking on the **Enable SSO** button.</span></span>

13. <span data-ttu-id="c38e2-197">Ahora, haga clic en el botón **Actualizar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="c38e2-197">Now click on the **Update** button so that all the settings are saved.</span></span> <span data-ttu-id="c38e2-198">Se generará el valor RelayState.</span><span class="sxs-lookup"><span data-stu-id="c38e2-198">This will generate the RelayState value.</span></span> <span data-ttu-id="c38e2-199">Copie el valor de RelayState, que se genera en el cuadro de texto y péguelo en el cuadro de texto **Estado de la retransmisión** en la sección **Dominio y direcciones URL de Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-199">Copy the RelayState value, which is generated in the text box, paste it in the **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="c38e2-200">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c38e2-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c38e2-201">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="c38e2-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c38e2-202">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c38e2-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c38e2-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c38e2-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="c38e2-204">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c38e2-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="c38e2-206">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="c38e2-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c38e2-207">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c38e2-209">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c38e2-211">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c38e2-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c38e2-213">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="c38e2-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c38e2-215">a.</span><span class="sxs-lookup"><span data-stu-id="c38e2-215">a.</span></span> <span data-ttu-id="c38e2-216">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c38e2-217">b.</span><span class="sxs-lookup"><span data-stu-id="c38e2-217">b.</span></span> <span data-ttu-id="c38e2-218">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c38e2-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c38e2-219">c.</span><span class="sxs-lookup"><span data-stu-id="c38e2-219">c.</span></span> <span data-ttu-id="c38e2-220">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c38e2-221">d.</span><span class="sxs-lookup"><span data-stu-id="c38e2-221">d.</span></span> <span data-ttu-id="c38e2-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="c38e2-223">Creación de un usuario de prueba de Lifesize Cloud</span><span class="sxs-lookup"><span data-stu-id="c38e2-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="c38e2-224">En esta sección, creará el usuario Britta Simon en Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="c38e2-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="c38e2-225">Lifesize Cloud no admite el aprovisionamiento de usuarios automático.</span><span class="sxs-lookup"><span data-stu-id="c38e2-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="c38e2-226">Después de autenticarse correctamente en Azure AD, el usuario se aprovisionará automáticamente en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c38e2-226">After successful authentication at Azure AD, the user will be automatically provisioned in the application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c38e2-227">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c38e2-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c38e2-228">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="c38e2-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lifesize Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="c38e2-230">**Para asignar Britta Simon a Lifesize Cloud, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="c38e2-230">**To assign Britta Simon to Lifesize Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="c38e2-231">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="c38e2-233">En la lista de aplicaciones, seleccione **Lifesize Cloud**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-233">In the applications list, select **Lifesize Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="c38e2-235">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="c38e2-237">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-237">Click **Add** button.</span></span> <span data-ttu-id="c38e2-238">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="c38e2-240">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="c38e2-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c38e2-241">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c38e2-242">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="c38e2-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c38e2-243">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="c38e2-243">Testing single sign-on</span></span>

<span data-ttu-id="c38e2-244">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="c38e2-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c38e2-245">Al hacer clic en el icono de Lifesize Cloud en el Panel de acceso, debería llegar a la página de inicio de sesión de la aplicación Lifesize Cloud.</span><span class="sxs-lookup"><span data-stu-id="c38e2-245">When you click the Lifesize Cloud tile in the Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="c38e2-246">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c38e2-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c38e2-247">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="c38e2-247">Additional resources</span></span>

* [<span data-ttu-id="c38e2-248">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c38e2-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c38e2-249">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c38e2-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

