---
title: "Tutorial: Integración de Azure Active Directory con TeamSeer | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="55e69-103">Tutorial: integración de Azure Active Directory con TeamSeer</span><span class="sxs-lookup"><span data-stu-id="55e69-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="55e69-104">En este tutorial, aprenderá a integrar TeamSeer con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55e69-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55e69-105">La integración de TeamSeer con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="55e69-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="55e69-106">En Azure AD se puede controlar quién tiene acceso a TeamSeer</span><span class="sxs-lookup"><span data-stu-id="55e69-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="55e69-107">Puede permitir que los usuarios inicien sesión automáticamente en TeamSeer (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e69-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55e69-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="55e69-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="55e69-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55e69-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55e69-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="55e69-110">Prerequisites</span></span>

<span data-ttu-id="55e69-111">Para configurar la integración de Azure AD con TeamSeer, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="55e69-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="55e69-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e69-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55e69-113">Una suscripción habilitada para el inicio de sesión único en TeamSeer</span><span class="sxs-lookup"><span data-stu-id="55e69-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55e69-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="55e69-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55e69-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="55e69-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55e69-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="55e69-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55e69-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55e69-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55e69-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="55e69-118">Scenario description</span></span>
<span data-ttu-id="55e69-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="55e69-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55e69-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="55e69-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55e69-121">Incorporación de TeamSeer desde la galería</span><span class="sxs-lookup"><span data-stu-id="55e69-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="55e69-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e69-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="55e69-123">Incorporación de TeamSeer desde la galería</span><span class="sxs-lookup"><span data-stu-id="55e69-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="55e69-124">Para configurar la integración de TeamSeer en Azure AD, será preciso que agregue TeamSeer desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="55e69-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="55e69-125">**Para agregar TeamSeer desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="55e69-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="55e69-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55e69-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55e69-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="55e69-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="55e69-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="55e69-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="55e69-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55e69-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="55e69-133">En el cuadro de búsqueda, escriba **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="55e69-133">In the search box, type **TeamSeer**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="55e69-135">En el panel de resultados, seleccione **TeamSeer** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55e69-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55e69-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e69-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55e69-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con TeamSeer con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55e69-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="55e69-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de TeamSeer para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55e69-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="55e69-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario asociado de TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="55e69-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="55e69-141">Para establecer la relación de vínculo, en TeamSeer, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="55e69-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="55e69-142">Para configurar y probar el inicio de sesión único de Azure AD con TeamSeer, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="55e69-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="55e69-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="55e69-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="55e69-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55e69-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55e69-145">**[Creación de un usuario de prueba de TeamSeer](#creating-a-teamseer-test-user)**: para tener un homólogo de Britta Simon en TeamSeer vinculado a la representación del usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55e69-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="55e69-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55e69-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55e69-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="55e69-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55e69-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e69-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55e69-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="55e69-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="55e69-150">**Para configurar el inicio de sesión único de Azure AD con TeamSeer, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="55e69-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="55e69-151">En Azure Portal, en la página de integración de la aplicación **TeamSeer**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="55e69-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="55e69-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="55e69-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="55e69-155">En la sección de **TeamSeer Domain and URLs** (Dominio y direcciones URL de TeamSeer), lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="55e69-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="55e69-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://www.teamseer.com/<companyid>`.</span><span class="sxs-lookup"><span data-stu-id="55e69-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55e69-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="55e69-158">The value is not real.</span></span> <span data-ttu-id="55e69-159">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="55e69-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="55e69-160">Póngase en contacto con el [equipo de soporte técnico de TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="55e69-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="55e69-161">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="55e69-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="55e69-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="55e69-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55e69-165">En la sección **TeamSeer Configuration** (Configuración de TeamSeer), haga clic en **Configure TeamSeer** (Configurar TeamSeer) para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="55e69-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="55e69-166">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="55e69-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="55e69-168">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de TeamSeer como administrador.</span><span class="sxs-lookup"><span data-stu-id="55e69-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="55e69-169">Vaya a **Administrador de RR. HH**.</span><span class="sxs-lookup"><span data-stu-id="55e69-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="55e69-170">![Administración de RR. HH.](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Administración de RR. HH.")</span><span class="sxs-lookup"><span data-stu-id="55e69-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="55e69-171">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="55e69-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="55e69-172">![Instalación](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="55e69-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="55e69-173">Haga clic en **Configurar detalles del proveedor SAML**.</span><span class="sxs-lookup"><span data-stu-id="55e69-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="55e69-174">![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="55e69-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="55e69-175">En la sección de detalles del proveedor SAML, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="55e69-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="55e69-176">![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="55e69-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="55e69-177">a.</span><span class="sxs-lookup"><span data-stu-id="55e69-177">a.</span></span> <span data-ttu-id="55e69-178">Pegue el valor de **Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único) en el cuadro de texto **URL**.</span><span class="sxs-lookup"><span data-stu-id="55e69-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="55e69-179">b.</span><span class="sxs-lookup"><span data-stu-id="55e69-179">b.</span></span> <span data-ttu-id="55e69-180">Abra el certificado codificado en base 64 en el bloc de notas, copie su contenido en el portapapeles y péguelo en el cuadro de texto **IdP Public Certificate** (Certificado público del proveedor de identidades).</span><span class="sxs-lookup"><span data-stu-id="55e69-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="55e69-181">Para completar la configuración del proveedor SAML, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="55e69-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="55e69-182">![Configuración de SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Configuración de SAML")</span><span class="sxs-lookup"><span data-stu-id="55e69-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="55e69-183">a.</span><span class="sxs-lookup"><span data-stu-id="55e69-183">a.</span></span> <span data-ttu-id="55e69-184">En las **Direcciones de correo electrónico de prueba**, escriba la dirección de correo electrónico del usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="55e69-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="55e69-185">b.</span><span class="sxs-lookup"><span data-stu-id="55e69-185">b.</span></span> <span data-ttu-id="55e69-186">En el cuadro de texto **Emisor** , escriba la dirección URL de emisor del proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="55e69-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="55e69-187">c.</span><span class="sxs-lookup"><span data-stu-id="55e69-187">c.</span></span> <span data-ttu-id="55e69-188">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="55e69-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="55e69-189">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="55e69-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="55e69-190">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="55e69-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="55e69-191">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55e69-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55e69-192">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e69-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="55e69-193">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="55e69-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="55e69-195">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="55e69-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="55e69-196">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="55e69-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55e69-198">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="55e69-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55e69-200">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55e69-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55e69-202">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="55e69-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55e69-204">a.</span><span class="sxs-lookup"><span data-stu-id="55e69-204">a.</span></span> <span data-ttu-id="55e69-205">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55e69-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55e69-206">b.</span><span class="sxs-lookup"><span data-stu-id="55e69-206">b.</span></span> <span data-ttu-id="55e69-207">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55e69-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55e69-208">c.</span><span class="sxs-lookup"><span data-stu-id="55e69-208">c.</span></span> <span data-ttu-id="55e69-209">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="55e69-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="55e69-210">d.</span><span class="sxs-lookup"><span data-stu-id="55e69-210">d.</span></span> <span data-ttu-id="55e69-211">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="55e69-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="55e69-212">Creación de un usuario de prueba de TeamSeer</span><span class="sxs-lookup"><span data-stu-id="55e69-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="55e69-213">Para permitir que los usuarios de Azure AD inicien sesión en TeamSeer, deben aprovisionarse en ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="55e69-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="55e69-214">En el caso de TeamSeer, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="55e69-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="55e69-215">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="55e69-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="55e69-216">Inicie sesión en su sitio de la compañía de **TeamSeer** como administrador.</span><span class="sxs-lookup"><span data-stu-id="55e69-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="55e69-217">Lleve a cabo los siguiente pasos:</span><span class="sxs-lookup"><span data-stu-id="55e69-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="55e69-218">![Administración de RR. HH.](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Administración de RR. HH.")</span><span class="sxs-lookup"><span data-stu-id="55e69-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="55e69-219">a.</span><span class="sxs-lookup"><span data-stu-id="55e69-219">a.</span></span> <span data-ttu-id="55e69-220">Vaya a **Administrador de RR. HH. \> Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="55e69-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="55e69-221">b.</span><span class="sxs-lookup"><span data-stu-id="55e69-221">b.</span></span> <span data-ttu-id="55e69-222">Haga clic en **Ejecutar el Asistente para nuevos usuarios**.</span><span class="sxs-lookup"><span data-stu-id="55e69-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="55e69-223">En la sección **Detalles del usuario** , lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="55e69-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="55e69-224">![Detalles del usuario](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Detalles del usuario")</span><span class="sxs-lookup"><span data-stu-id="55e69-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="55e69-225">a.</span><span class="sxs-lookup"><span data-stu-id="55e69-225">a.</span></span> <span data-ttu-id="55e69-226">Escriba el **Nombre**, **Apellido**, **Nombre de usuario (dirección de correo electrónico)** de una cuenta válida de AAD que desee aprovisionar en los cuadros de texto correspondientes.</span><span class="sxs-lookup"><span data-stu-id="55e69-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="55e69-227">b.</span><span class="sxs-lookup"><span data-stu-id="55e69-227">b.</span></span> <span data-ttu-id="55e69-228">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="55e69-228">Click **Next**.</span></span>

4. <span data-ttu-id="55e69-229">Siga las instrucciones en pantalla para agregar un nuevo usuario y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="55e69-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="55e69-230">Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de TeamSeer ofrecida por TeamSeer para aprovisionar cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55e69-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="55e69-231">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e69-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="55e69-232">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="55e69-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="55e69-234">**Para asignar a Britta Simon a TeamSeer, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="55e69-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="55e69-235">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="55e69-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="55e69-237">En la lista de aplicaciones, seleccione **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="55e69-237">In the applications list, select **TeamSeer**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="55e69-239">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="55e69-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="55e69-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="55e69-241">Click **Add** button.</span></span> <span data-ttu-id="55e69-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="55e69-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="55e69-244">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="55e69-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="55e69-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="55e69-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55e69-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="55e69-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="55e69-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="55e69-247">Testing single sign-on</span></span>

<span data-ttu-id="55e69-248">Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="55e69-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="55e69-249">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55e69-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55e69-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="55e69-250">Additional resources</span></span>

* [<span data-ttu-id="55e69-251">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55e69-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55e69-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55e69-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

