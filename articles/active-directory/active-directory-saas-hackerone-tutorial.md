---
title: "Tutorial: Integración de Azure Active Directory con HackerOne | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y HackerOne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="b47a1-103">Tutorial: Integración de Azure Active Directory con HackerOne</span><span class="sxs-lookup"><span data-stu-id="b47a1-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="b47a1-104">En este tutorial se aprende a integrar HackerOne con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b47a1-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b47a1-105">La integración de HackerOne con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b47a1-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b47a1-106">Puede controlar en Azure AD quién tiene acceso a HackerOne.</span><span class="sxs-lookup"><span data-stu-id="b47a1-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="b47a1-107">Puede permitir que los usuarios inicien sesión automáticamente en HackerOne (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b47a1-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b47a1-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b47a1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b47a1-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b47a1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b47a1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b47a1-110">Prerequisites</span></span>

<span data-ttu-id="b47a1-111">Para configurar la integración de Azure AD con HackerOne, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b47a1-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="b47a1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b47a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b47a1-113">Una suscripción habilitada para el inicio de sesión único en HackerOne</span><span class="sxs-lookup"><span data-stu-id="b47a1-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b47a1-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b47a1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b47a1-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b47a1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b47a1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b47a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b47a1-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b47a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b47a1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b47a1-118">Scenario description</span></span>
<span data-ttu-id="b47a1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b47a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b47a1-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b47a1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b47a1-121">Incorporación de HackerOne desde la galería</span><span class="sxs-lookup"><span data-stu-id="b47a1-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="b47a1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b47a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="b47a1-123">Incorporación de HackerOne desde la galería</span><span class="sxs-lookup"><span data-stu-id="b47a1-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="b47a1-124">Para configurar la integración de HackerOne en Azure AD, será preciso que agregue HackerOne desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b47a1-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b47a1-125">**Para agregar HackerOne desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b47a1-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b47a1-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b47a1-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b47a1-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b47a1-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b47a1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b47a1-133">En el cuadro de búsqueda, escriba **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-133">In the search box, type **HackerOne**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="b47a1-135">En el panel de resultados, seleccione **HackerOne** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b47a1-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b47a1-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b47a1-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b47a1-138">En esta sección se configura y prueba el inicio de sesión único de Azure AD con HackerOne con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b47a1-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b47a1-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de HackerOne para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b47a1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="b47a1-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de HackerOne.</span><span class="sxs-lookup"><span data-stu-id="b47a1-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="b47a1-141">Para establecer la relación de vínculo, en HackerOne, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b47a1-142">Para configurar y probar el inicio de sesión único de Azure AD con HackerOne, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b47a1-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b47a1-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b47a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b47a1-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b47a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b47a1-145">**[Creación de un usuario de prueba de HackerOne](#creating-a-hackerone-test-user)**: para tener un homólogo de Britta Simon en HackerOne vinculado a la representación de usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b47a1-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b47a1-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b47a1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b47a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b47a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b47a1-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b47a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b47a1-149">En esta sección se habilita el inicio de sesión único de Azure AD en Azure Portal y se configura el inicio de sesión único en la aplicación HackerOne.</span><span class="sxs-lookup"><span data-stu-id="b47a1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="b47a1-150">**Para configurar el inicio de sesión único de Azure AD con HackerOne, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b47a1-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="b47a1-151">En Azure Portal, en la página de integración de la aplicación **HackerOne**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b47a1-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b47a1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="b47a1-155">En la sección de **dirección URL de inicio de sesión único e identificador de HackerOne**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b47a1-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="b47a1-157">a.</span><span class="sxs-lookup"><span data-stu-id="b47a1-157">a.</span></span> <span data-ttu-id="b47a1-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://hackerone.com/<company name>/authentication`.</span><span class="sxs-lookup"><span data-stu-id="b47a1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="b47a1-159">b.</span><span class="sxs-lookup"><span data-stu-id="b47a1-159">b.</span></span> <span data-ttu-id="b47a1-160">En el cuadro de texto **Identificador**, escriba una dirección URL como: `https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="b47a1-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b47a1-161">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="b47a1-161">This value is not real.</span></span> <span data-ttu-id="b47a1-162">Actualícelo con la dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="b47a1-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b47a1-163">Contacte con el [equipo de soporte técnico de HackerOne](mailto:support@hackerone.com) para obtener este valor.</span><span class="sxs-lookup"><span data-stu-id="b47a1-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="b47a1-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b47a1-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="b47a1-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b47a1-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b47a1-168">En la sección **Configuración de HackerOne**, haga clic en **Configurar HackerOne** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b47a1-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="b47a1-171">Inicie sesión en el inquilino de HackerOne como administrador.</span><span class="sxs-lookup"><span data-stu-id="b47a1-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="b47a1-172">En el menú de la parte superior, haga clic en "**Settings**" (Configuración).</span><span class="sxs-lookup"><span data-stu-id="b47a1-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="b47a1-174">Vaya a "**Authentication**" (Autenticación) y haga clic en el botón "**Add SAML settings**" (Agregar configuración de SAML).</span><span class="sxs-lookup"><span data-stu-id="b47a1-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="b47a1-176">En el cuadro de diálogo **SAML Settings** (Configuración de SAML), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b47a1-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="b47a1-178">a.</span><span class="sxs-lookup"><span data-stu-id="b47a1-178">a.</span></span> <span data-ttu-id="b47a1-179">En el cuadro de texto **Dominio de correo electrónico** , escriba un dominio registrado.</span><span class="sxs-lookup"><span data-stu-id="b47a1-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="b47a1-180">b.</span><span class="sxs-lookup"><span data-stu-id="b47a1-180">b.</span></span> <span data-ttu-id="b47a1-181">En el cuadro de texto **Single Sign On URL** (Dirección URL de inicio de sesión), pegue el valor de la **dirección URL del servicio de inicio de sesión único de SAML** que ha copiado de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b47a1-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b47a1-182">c.</span><span class="sxs-lookup"><span data-stu-id="b47a1-182">c.</span></span> <span data-ttu-id="b47a1-183">Abra el **archivo de certificado** que descargó de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado X509**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="b47a1-184">d.</span><span class="sxs-lookup"><span data-stu-id="b47a1-184">d.</span></span> <span data-ttu-id="b47a1-185">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-185">Click **Save**.</span></span>

11. <span data-ttu-id="b47a1-186">En el diálogo Configuración de autenticación, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b47a1-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="b47a1-188">a.</span><span class="sxs-lookup"><span data-stu-id="b47a1-188">a.</span></span> <span data-ttu-id="b47a1-189">Haga clic en **Ejecutar prueba**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-189">Click **Run test**.</span></span>

    <span data-ttu-id="b47a1-190">b.</span><span class="sxs-lookup"><span data-stu-id="b47a1-190">b.</span></span> <span data-ttu-id="b47a1-191">Si el valor del campo **Status** (Estado) es igual a **Last test status: created** (Último estado de la prueba: creado), contacte con el [equipo de soporte técnico de HackerOne](mailto:support@hackerone.com) para pedir una revisión de la configuración.</span><span class="sxs-lookup"><span data-stu-id="b47a1-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="b47a1-192">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b47a1-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b47a1-193">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b47a1-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b47a1-194">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b47a1-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b47a1-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b47a1-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="b47a1-196">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b47a1-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b47a1-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b47a1-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b47a1-199">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b47a1-201">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b47a1-203">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b47a1-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b47a1-205">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b47a1-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b47a1-207">a.</span><span class="sxs-lookup"><span data-stu-id="b47a1-207">a.</span></span> <span data-ttu-id="b47a1-208">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b47a1-209">b.</span><span class="sxs-lookup"><span data-stu-id="b47a1-209">b.</span></span> <span data-ttu-id="b47a1-210">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b47a1-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b47a1-211">c.</span><span class="sxs-lookup"><span data-stu-id="b47a1-211">c.</span></span> <span data-ttu-id="b47a1-212">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b47a1-213">d.</span><span class="sxs-lookup"><span data-stu-id="b47a1-213">d.</span></span> <span data-ttu-id="b47a1-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="b47a1-215">Creación de un usuario de prueba de HackerOne</span><span class="sxs-lookup"><span data-stu-id="b47a1-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="b47a1-216">A continuación, creará un usuario llamado Simon Britta en HackerOne.</span><span class="sxs-lookup"><span data-stu-id="b47a1-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="b47a1-217">HackerOne admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="b47a1-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="b47a1-218">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="b47a1-218">There is no action item for you in this section.</span></span> <span data-ttu-id="b47a1-219">Al acceder a HackerOne, se crea un usuario nuevo si todavía no existe uno.</span><span class="sxs-lookup"><span data-stu-id="b47a1-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="b47a1-220">Si necesita crear manualmente un usuario, debe ponerse en contacto con el equipo de soporte técnico de Certify.</span><span class="sxs-lookup"><span data-stu-id="b47a1-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b47a1-221">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b47a1-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b47a1-222">En esta sección se habilita a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a HackerOne.</span><span class="sxs-lookup"><span data-stu-id="b47a1-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b47a1-224">**Para asignar a Britta Simon a HackerOne, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="b47a1-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="b47a1-225">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b47a1-227">En la lista de aplicaciones, seleccione **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-227">In the applications list, select **HackerOne**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="b47a1-229">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b47a1-231">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-231">Click **Add** button.</span></span> <span data-ttu-id="b47a1-232">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b47a1-234">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b47a1-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b47a1-235">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b47a1-236">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b47a1-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b47a1-237">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b47a1-237">Testing single sign-on</span></span>

<span data-ttu-id="b47a1-238">Por último, probará la configuración de inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b47a1-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="b47a1-239">Al hacer clic en el icono de HackerOne en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación HackerOne.</span><span class="sxs-lookup"><span data-stu-id="b47a1-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b47a1-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b47a1-240">Additional resources</span></span>

* [<span data-ttu-id="b47a1-241">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b47a1-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b47a1-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b47a1-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

