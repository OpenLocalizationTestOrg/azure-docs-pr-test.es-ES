---
title: "Tutorial: Integración de Azure Active Directory con PurelyHR | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="0eb72-103">Tutorial: Integración de Azure Active Directory con PurelyHR</span><span class="sxs-lookup"><span data-stu-id="0eb72-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="0eb72-104">En este tutorial, aprenderá a integrar PurelyHR con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0eb72-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0eb72-105">La integración de Pantheon con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="0eb72-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0eb72-106">Puede controlar en Azure AD quién tiene acceso a PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="0eb72-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="0eb72-107">Puede habilitar que los usuarios inicien sesión automáticamente en PurelyHR (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0eb72-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0eb72-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0eb72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0eb72-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0eb72-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0eb72-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0eb72-110">Prerequisites</span></span>

<span data-ttu-id="0eb72-111">Para configurar la integración de Azure AD con PurelyHR, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="0eb72-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="0eb72-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0eb72-113">Una suscripción habilitada para inicio de sesión único en PurelyHR</span><span class="sxs-lookup"><span data-stu-id="0eb72-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0eb72-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="0eb72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0eb72-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="0eb72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0eb72-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0eb72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0eb72-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0eb72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0eb72-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="0eb72-118">Scenario description</span></span>
<span data-ttu-id="0eb72-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="0eb72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0eb72-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="0eb72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0eb72-121">Adición de PurelyHR desde la galería</span><span class="sxs-lookup"><span data-stu-id="0eb72-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="0eb72-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="0eb72-123">Adición de PurelyHR desde la galería</span><span class="sxs-lookup"><span data-stu-id="0eb72-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="0eb72-124">Para configurar la integración de PurelyHR en Azure AD, deberá agregarlo desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="0eb72-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0eb72-125">**Para agregar Trakstar desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0eb72-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0eb72-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0eb72-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0eb72-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="0eb72-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0eb72-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="0eb72-133">En el cuadro de búsqueda, escriba **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-133">In the search box, type **PurelyHR**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="0eb72-135">En el panel de resultados, seleccione **PurelyHR** y, luego, haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eb72-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0eb72-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0eb72-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con PurelyHR con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0eb72-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0eb72-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de PurelyHR para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0eb72-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="0eb72-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="0eb72-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="0eb72-141">Para establecer la relación de vínculo, en PurelyHR, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0eb72-142">Para configurar y probar el inicio de sesión único de Azure AD con PurelyHR, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="0eb72-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0eb72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="0eb72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0eb72-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0eb72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0eb72-145">**[Creación de un usuario de prueba de PurelyHR](#creating-a-purelyhr-test-user)**: para tener un homólogo de Britta Simon en PurelyHR que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="0eb72-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0eb72-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0eb72-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0eb72-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="0eb72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0eb72-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0eb72-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="0eb72-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="0eb72-150">**Para configurar el inicio de sesión único de Azure AD con PurelyHR, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0eb72-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="0eb72-151">En Azure Portal, en la página de integración de la aplicación **PurelyHR**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="0eb72-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="0eb72-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="0eb72-155">En la sección **Dominio y direcciones URL de PurelyHR**, realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:</span><span class="sxs-lookup"><span data-stu-id="0eb72-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="0eb72-157">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<companyID>.purelyhr.com/sso-consume`.</span><span class="sxs-lookup"><span data-stu-id="0eb72-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="0eb72-158">Active **Mostrar configuración avanzada de URL**, si desea volver a configurar la aplicación en modo iniciado por **SP**:</span><span class="sxs-lookup"><span data-stu-id="0eb72-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="0eb72-160">En el cuadro de texto **URL de inicio de sesión**, escriba el valor con el siguiente patrón: `https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="0eb72-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="0eb72-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="0eb72-161">These values are not the real.</span></span> <span data-ttu-id="0eb72-162">Actualice estos valores con los valores reales de URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="0eb72-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="0eb72-163">Póngase en contacto con el [equipo de soporte técnico de PurelyHR](http://support.purelyhr.com/) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="0eb72-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="0eb72-164">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="0eb72-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="0eb72-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="0eb72-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0eb72-168">En la sección **Configuración de PurelyHR**, haga clic en **Configurar PurelyHR** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0eb72-169">Copie **SAML Entity ID and SAML Single Sign-On Service URL** (URL del servicio de inicio de sesión único de SAML e Identificador de entidad de SAML) de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="0eb72-171">Para configurar el inicio de sesión único en **PurelyHR**, inicie sesión en su sitio web como administrador.</span><span class="sxs-lookup"><span data-stu-id="0eb72-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="0eb72-172">Abra el **panel** en las opciones de la barra de herramientas y haga clic en **SSO Settings** (Configuración de SSO).</span><span class="sxs-lookup"><span data-stu-id="0eb72-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="0eb72-173">Pegue los valores en los cuadros tal y como se describe a continuación:</span><span class="sxs-lookup"><span data-stu-id="0eb72-173">Paste the values in the boxes as described below-</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="0eb72-175">a.</span><span class="sxs-lookup"><span data-stu-id="0eb72-175">a.</span></span> <span data-ttu-id="0eb72-176">Abra el archivo **Certificate(Bas64)** que se ha descargado de Azure Portal en el bloc de notas y copie el valor del certificado.</span><span class="sxs-lookup"><span data-stu-id="0eb72-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="0eb72-177">Pegue el valor copiado en el cuadro **X.509 Certificate** (Certificado X.509).</span><span class="sxs-lookup"><span data-stu-id="0eb72-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="0eb72-178">b.</span><span class="sxs-lookup"><span data-stu-id="0eb72-178">b.</span></span> <span data-ttu-id="0eb72-179">En el cuadro **IdP Issuer URL** (URL del emisor de IdP), pegue el **identificador de entidad de SAML** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0eb72-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="0eb72-180">c.</span><span class="sxs-lookup"><span data-stu-id="0eb72-180">c.</span></span> <span data-ttu-id="0eb72-181">En el cuadro **Idp Endpoint URL** (URL de punto de conexión de IdP), pegue la **URL del servicio de inicio de sesión único de SAML** que copió de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0eb72-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="0eb72-182">d.</span><span class="sxs-lookup"><span data-stu-id="0eb72-182">d.</span></span> <span data-ttu-id="0eb72-183">Active la casilla **Auto-Create Users** (Creación automática de usuarios) para habilitar el aprovisionamiento automático de usuarios en PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="0eb72-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="0eb72-184">e.</span><span class="sxs-lookup"><span data-stu-id="0eb72-184">e.</span></span> <span data-ttu-id="0eb72-185">Haga clic en **Guardar cambios** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="0eb72-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="0eb72-186">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0eb72-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0eb72-187">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="0eb72-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0eb72-188">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0eb72-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0eb72-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb72-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="0eb72-190">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0eb72-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="0eb72-192">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="0eb72-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0eb72-193">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0eb72-195">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0eb72-197">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0eb72-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0eb72-199">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="0eb72-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0eb72-201">a.</span><span class="sxs-lookup"><span data-stu-id="0eb72-201">a.</span></span> <span data-ttu-id="0eb72-202">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0eb72-203">b.</span><span class="sxs-lookup"><span data-stu-id="0eb72-203">b.</span></span> <span data-ttu-id="0eb72-204">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0eb72-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0eb72-205">c.</span><span class="sxs-lookup"><span data-stu-id="0eb72-205">c.</span></span> <span data-ttu-id="0eb72-206">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0eb72-207">d.</span><span class="sxs-lookup"><span data-stu-id="0eb72-207">d.</span></span> <span data-ttu-id="0eb72-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="0eb72-209">Creación de un usuario de prueba en PurelyHR</span><span class="sxs-lookup"><span data-stu-id="0eb72-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="0eb72-210">Para permitir que los usuarios de Azure AD inicien sesión en PurelyHR, tienen que aprovisionarse en esta solución.</span><span class="sxs-lookup"><span data-stu-id="0eb72-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="0eb72-211">En PurelyHR, el aprovisionamiento es una tarea automática y no se requieren pasos manuales al habilitar el aprovisionamiento automático de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0eb72-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0eb72-212">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0eb72-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0eb72-213">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="0eb72-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="0eb72-215">**Para asignar a Britta Simon a PurelyHR, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="0eb72-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="0eb72-216">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="0eb72-218">En la lista de aplicaciones, seleccione **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-218">In the applications list, select **PurelyHR**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="0eb72-220">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="0eb72-222">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-222">Click **Add** button.</span></span> <span data-ttu-id="0eb72-223">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="0eb72-225">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="0eb72-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0eb72-226">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0eb72-227">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="0eb72-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0eb72-228">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="0eb72-228">Testing single sign-on</span></span>

<span data-ttu-id="0eb72-229">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="0eb72-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0eb72-230">Al hacer clic en el icono de Absorb LMS del panel de acceso, inicia sesión automáticamente en su aplicación Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="0eb72-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="0eb72-231">Para obtener más información sobre el panel de acceso, consulte</span><span class="sxs-lookup"><span data-stu-id="0eb72-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="0eb72-232">[Introducción al panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0eb72-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0eb72-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="0eb72-233">Additional resources</span></span>

* [<span data-ttu-id="0eb72-234">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0eb72-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0eb72-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0eb72-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

