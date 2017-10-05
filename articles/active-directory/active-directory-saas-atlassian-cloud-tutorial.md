---
title: "Tutorial: Integración de Azure Active Directory con Atlassian Cloud | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Atlassian Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="88c09-103">Tutorial: Integración de Azure Active Directory con Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="88c09-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="88c09-104">En este tutorial, aprenderá a integrar Atlassian Cloud con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88c09-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88c09-105">La integración de Atlassian Cloud con Azure AD ofrece las ventajas siguientes:</span><span class="sxs-lookup"><span data-stu-id="88c09-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88c09-106">En Azure AD se puede controlar quién tiene acceso a Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="88c09-107">Puede permitir que los usuarios inicien sesión automáticamente en Atlassian Cloud (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c09-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88c09-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="88c09-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88c09-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88c09-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88c09-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="88c09-110">Prerequisites</span></span>

<span data-ttu-id="88c09-111">Para configurar la integración de Azure AD con Atlassian Cloud se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="88c09-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="88c09-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c09-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88c09-113">Una suscripción habilitada para el inicio de sesión único en Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="88c09-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88c09-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="88c09-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88c09-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="88c09-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88c09-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="88c09-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88c09-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88c09-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88c09-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="88c09-118">Scenario description</span></span>
<span data-ttu-id="88c09-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="88c09-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88c09-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="88c09-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88c09-121">Incorporación de Atlassian Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="88c09-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="88c09-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c09-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="88c09-123">Incorporación de Atlassian Cloud desde la galería</span><span class="sxs-lookup"><span data-stu-id="88c09-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="88c09-124">Para configurar la integración de Atlassian Cloud en Azure AD, necesita agregar Atlassian Cloud desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="88c09-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88c09-125">**Para agregar Atlassian Cloud desde la galería, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="88c09-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88c09-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88c09-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88c09-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="88c09-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88c09-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="88c09-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="88c09-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88c09-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="88c09-133">En el cuadro de búsqueda, escriba **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="88c09-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="88c09-135">En el panel de resultados, seleccione **Atlassian Cloud** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88c09-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88c09-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c09-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88c09-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Atlassian Cloud con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88c09-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88c09-139">Para que el inicio de sesión único funcione, Azure AD necesita saber cuál es el usuario homólogo de Atlassian Cloud para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c09-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="88c09-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="88c09-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="88c09-142">Para configurar y probar el inicio de sesión único de Azure AD con Atlassian Cloud, es necesario completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="88c09-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88c09-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="88c09-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88c09-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88c09-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88c09-145">**[Creación de un usuario de prueba en Atlassian Cloud](#creating-an-atlassian-cloud-test-user)**: para tener un homólogo de Britta Simon en Atlassian Cloud que esté vinculado a su representación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c09-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="88c09-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88c09-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88c09-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="88c09-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88c09-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c09-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88c09-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure portal y configurará el inicio de sesión único en la aplicación Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="88c09-150">**Para configurar el inicio de sesión único de Azure AD con Atlassian Cloud, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="88c09-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="88c09-151">En la página de integración de la aplicación **Atlassian Cloud** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="88c09-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="88c09-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="88c09-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="88c09-155">En la sección **Dominio y direcciones URL de Atlassian Cloud**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="88c09-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="88c09-157">a.</span><span class="sxs-lookup"><span data-stu-id="88c09-157">a.</span></span> <span data-ttu-id="88c09-158">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="88c09-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="88c09-159">b.</span><span class="sxs-lookup"><span data-stu-id="88c09-159">b.</span></span> <span data-ttu-id="88c09-160">En el cuadro de texto **URL de respuesta**, escriba una dirección URL como: `https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="88c09-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="88c09-161">Active **Mostrar configuración avanzada de URL** y siga estos pasos si desea configurar la aplicación en el modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="88c09-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="88c09-163">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.atlassian.net`.</span><span class="sxs-lookup"><span data-stu-id="88c09-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88c09-164">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="88c09-164">These values are not real.</span></span> <span data-ttu-id="88c09-165">Actualice estos valores con el identificador y la dirección URL de inicio de sesión reales.</span><span class="sxs-lookup"><span data-stu-id="88c09-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="88c09-166">Puede obtener los valores exactos desde la pantalla de configuración de SAML de Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="88c09-167">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="88c09-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="88c09-169">En la sección **Configuración de Atlassian Cloud**, haga clic en **Configurar Atlassian Cloud** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="88c09-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="88c09-170">Copie **SAML Entity ID and SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML e Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="88c09-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="88c09-172">Para configurar el inicio de sesión único de la aplicación, inicie sesión en el portal de Atlassian mediante los derechos de administrador.</span><span class="sxs-lookup"><span data-stu-id="88c09-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="88c09-173">En la sección Autenticación del panel de navegación izquierdo, haga clic en **Dominios**.</span><span class="sxs-lookup"><span data-stu-id="88c09-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="88c09-175">a.</span><span class="sxs-lookup"><span data-stu-id="88c09-175">a.</span></span> <span data-ttu-id="88c09-176">En el cuadro de texto, escriba el nombre de dominio y, a continuación, haga clic en **Agregar dominio**.</span><span class="sxs-lookup"><span data-stu-id="88c09-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="88c09-178">b.</span><span class="sxs-lookup"><span data-stu-id="88c09-178">b.</span></span> <span data-ttu-id="88c09-179">Para comprobar el dominio, haga clic en **Comprobar**.</span><span class="sxs-lookup"><span data-stu-id="88c09-179">To verify the domain, click **Verify**.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="88c09-181">c.</span><span class="sxs-lookup"><span data-stu-id="88c09-181">c.</span></span> <span data-ttu-id="88c09-182">Descargue el archivo html de comprobación de dominio, cárguelo en la carpeta raíz del sitio web del dominio y, a continuación, haga clic en **Comprobar dominio**.</span><span class="sxs-lookup"><span data-stu-id="88c09-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="88c09-184">d.</span><span class="sxs-lookup"><span data-stu-id="88c09-184">d.</span></span> <span data-ttu-id="88c09-185">Una vez comprobado el dominio, el valor del campo **Estado** será **Comprobado**.</span><span class="sxs-lookup"><span data-stu-id="88c09-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="88c09-187">En la barra de navegación de la izquierda, haga clic en **SAML**.</span><span class="sxs-lookup"><span data-stu-id="88c09-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="88c09-189">Cree una configuración de SAML y agregue la configuración del proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="88c09-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="88c09-191">a.</span><span class="sxs-lookup"><span data-stu-id="88c09-191">a.</span></span> <span data-ttu-id="88c09-192">En el cuadro de texto **Identity Provider Entity ID)** (Identificador de entidad del proveedor de identidades), pegue el valor del **identificador de entidad de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="88c09-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="88c09-193">b.</span><span class="sxs-lookup"><span data-stu-id="88c09-193">b.</span></span> <span data-ttu-id="88c09-194">En el cuadro de texto **Identity provider SSO URL** (Dirección URL de inicio de sesión único del proveedor de identidades), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML**, que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="88c09-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="88c09-195">c.</span><span class="sxs-lookup"><span data-stu-id="88c09-195">c.</span></span> <span data-ttu-id="88c09-196">Abra el certificado descargado de Azure Portal, copie los valores sin las líneas de inicio y fin y péguelos en el cuadro **Certificado Public X509**.</span><span class="sxs-lookup"><span data-stu-id="88c09-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="88c09-197">d.</span><span class="sxs-lookup"><span data-stu-id="88c09-197">d.</span></span> <span data-ttu-id="88c09-198">Para guardar la configuración, haga clic en **Guardar configuración**.</span><span class="sxs-lookup"><span data-stu-id="88c09-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="88c09-199">Actualice la configuración de Azure AD para asegurarse de que ha configurado correctamente la dirección URL de identificador.</span><span class="sxs-lookup"><span data-stu-id="88c09-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="88c09-200">a.</span><span class="sxs-lookup"><span data-stu-id="88c09-200">a.</span></span> <span data-ttu-id="88c09-201">Copie el **identificador de identidad de SP** desde la pantalla de SAML y péguelo en Azure AD como valor del **identificador**.</span><span class="sxs-lookup"><span data-stu-id="88c09-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="88c09-202">b.</span><span class="sxs-lookup"><span data-stu-id="88c09-202">b.</span></span> <span data-ttu-id="88c09-203">La dirección URL de inicio de sesión es la dirección URL del inquilino de Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="88c09-205">En Azure Portal, haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="88c09-205">In the Azure portal, Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="88c09-207">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88c09-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="88c09-208">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="88c09-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="88c09-209">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88c09-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88c09-210">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c09-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="88c09-211">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88c09-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="88c09-213">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="88c09-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88c09-214">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88c09-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88c09-216">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="88c09-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88c09-218">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88c09-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88c09-220">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="88c09-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88c09-222">a.</span><span class="sxs-lookup"><span data-stu-id="88c09-222">a.</span></span> <span data-ttu-id="88c09-223">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88c09-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88c09-224">b.</span><span class="sxs-lookup"><span data-stu-id="88c09-224">b.</span></span> <span data-ttu-id="88c09-225">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88c09-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88c09-226">c.</span><span class="sxs-lookup"><span data-stu-id="88c09-226">c.</span></span> <span data-ttu-id="88c09-227">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="88c09-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88c09-228">d.</span><span class="sxs-lookup"><span data-stu-id="88c09-228">d.</span></span> <span data-ttu-id="88c09-229">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="88c09-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="88c09-230">Creación de un usuario de prueba de Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="88c09-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="88c09-231">Para permitir que los usuarios de Azure AD inicien sesión en Atlassian Cloud, tienen que aprovisionarse en Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="88c09-232">En el caso de Atlassian Cloud, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="88c09-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="88c09-233">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="88c09-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="88c09-234">En la sección de administración del sitio, haga clic en el botón **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="88c09-234">In the Site administration section, click the **Users** button</span></span>

    ![Creación de un usuario de Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="88c09-236">Haga clic en el botón **Create User** (Crear usuario) para crear un usuario en Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Creación de un usuario de Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="88c09-238">Escriba la **dirección de correo electrónico** del usuario, el **nombre de usuario** y el **nombre completo** y asigne el acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="88c09-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![Creación de un usuario de Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="88c09-240">Haga clic en el botón **Create user** (Crear usuario); se enviará la invitación de correo electrónico al usuario y, cuando acepte la invitación, el usuario estará activo en el sistema.</span><span class="sxs-lookup"><span data-stu-id="88c09-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="88c09-241">También puede crear usuarios de forma masiva haciendo clic en el botón **Bulk Create** (Crear de forma masiva) en la sección de usuarios.</span><span class="sxs-lookup"><span data-stu-id="88c09-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88c09-242">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="88c09-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88c09-243">En esta sección, va a conceder acceso a Britta Simon a Atlassian Cloud para que use el inicio de sesión único de Azure.</span><span class="sxs-lookup"><span data-stu-id="88c09-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="88c09-245">**Para asignar Britta Simon a Atlassian Cloud, siga este procedimiento:**</span><span class="sxs-lookup"><span data-stu-id="88c09-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="88c09-246">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="88c09-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="88c09-248">En la lista de aplicaciones, seleccione **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="88c09-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="88c09-250">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="88c09-250">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="88c09-252">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="88c09-252">Click **Add** button.</span></span> <span data-ttu-id="88c09-253">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="88c09-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="88c09-255">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="88c09-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88c09-256">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="88c09-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88c09-257">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="88c09-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88c09-258">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="88c09-258">Testing single sign-on</span></span>

<span data-ttu-id="88c09-259">En esta sección, probará la configuración de SSO de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="88c09-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="88c09-260">Al hacer clic en el icono de Atlassian Cloud en el panel de acceso, debería iniciar sesión automáticamente en la aplicación Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="88c09-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="88c09-261">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88c09-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88c09-262">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="88c09-262">Additional resources</span></span>

* [<span data-ttu-id="88c09-263">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88c09-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88c09-264">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88c09-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

