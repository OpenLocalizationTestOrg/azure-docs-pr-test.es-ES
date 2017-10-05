---
title: "Tutorial: Integración de Azure Active Directory con SensoScientific Wireless Temperature Monitoring System | Documentos de Microsoft"
description: "Obtenga información sobre cómo configurar un inicio de sesión único entre Azure Active Directory y SensoScientific Wireless Temperature Monitoring System."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: fa6242cf7f9559ca394ffde2e5e734cb935b03dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="a3245-103">Tutorial: Integración de Azure Active Directory con SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="a3245-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="a3245-104">En este tutorial, aprenderá a integrar SensoScientific Wireless Temperature Monitoring System con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a3245-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a3245-105">La integración de SensoScientific Wireless Temperature Monitoring System con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="a3245-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a3245-106">En Azure AD puede controlar quién accede a SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="a3245-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="a3245-107">Puede habilitar que los usuarios inicien sesión automáticamente en SensoScientific Wireless Temperature Monitoring System (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3245-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a3245-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a3245-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a3245-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a3245-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3245-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a3245-110">Prerequisites</span></span>

<span data-ttu-id="a3245-111">Para configurar la integración de Azure AD con SensoScientific Wireless Temperature Monitoring System, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a3245-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span></span>

- <span data-ttu-id="a3245-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3245-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a3245-113">Una suscripción que tenga habilitado el inicio de sesión único en SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="a3245-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a3245-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="a3245-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a3245-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="a3245-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a3245-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a3245-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a3245-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3245-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a3245-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="a3245-118">Scenario description</span></span>
<span data-ttu-id="a3245-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="a3245-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a3245-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="a3245-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a3245-121">Adición de SensoScientific Wireless Temperature Monitoring System desde la galería</span><span class="sxs-lookup"><span data-stu-id="a3245-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
2. <span data-ttu-id="a3245-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3245-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a><span data-ttu-id="a3245-123">Adición de SensoScientific Wireless Temperature Monitoring System desde la galería</span><span class="sxs-lookup"><span data-stu-id="a3245-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
<span data-ttu-id="a3245-124">Para configurar la integración de SensoScientific Wireless Temperature Monitoring System en Azure AD, debe agregar dicho sistema desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="a3245-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a3245-125">**Para agregar SensoScientific Wireless Temperature Monitoring System desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a3245-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a3245-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3245-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a3245-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="a3245-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a3245-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a3245-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="a3245-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3245-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="a3245-133">En el cuadro de búsqueda, escriba **SensoScientific Wireless Temperature Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="a3245-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="a3245-135">En el panel de resultados, seleccione **SensoScientific Wireless Temperature Monitoring System** y después haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3245-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a3245-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3245-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a3245-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SensoScientific Wireless Temperature Monitoring System mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a3245-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a3245-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de SensoScientific Wireless Temperature Monitoring System para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3245-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span></span> <span data-ttu-id="a3245-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="a3245-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span></span>

<span data-ttu-id="a3245-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="a3245-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="a3245-142">Para configurar y probar el inicio de sesión único de Azure AD con SensoScientific Wireless Temperature Monitoring System, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="a3245-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a3245-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="a3245-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a3245-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3245-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a3245-145">**[Creación de un usuario de prueba de SensoScientific Wireless Temperature Monitoring System](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**: para encontrar un homólogo de Britta Simon en SensoScientific Wireless Temperature Monitoring System vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3245-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a3245-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3245-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a3245-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="a3245-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a3245-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3245-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a3245-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="a3245-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="a3245-150">**Para configurar el inicio de sesión único de Azure AD con SensoScientific Wireless Temperature Monitoring System, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a3245-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="a3245-151">En la página de integración de la aplicación **SensoScientific Wireless Temperature Monitoring System** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="a3245-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="a3245-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a3245-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="a3245-155">En la sección **Dominio y direcciones URL de SensoScientific Wireless Temperature Monitoring System**, no necesita seguir ningún paso, ya que la aplicación ya está integrada previamente en Azure:</span><span class="sxs-lookup"><span data-stu-id="a3245-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="a3245-157">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a3245-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="a3245-159">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="a3245-159">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a3245-161">En la sección **Configuración de SensoScientific Wireless Temperature Monitoring System**, haga clic en **Configurar SensoScientific Wireless Temperature Monitoring System** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="a3245-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a3245-162">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad en SAML** y la **dirección URL de cierre de sesión** de la **sección Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="a3245-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="a3245-164">Inicie sesión en la aplicación SensoScientific Wireless Temperature Monitoring System como administrador.</span><span class="sxs-lookup"><span data-stu-id="a3245-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="a3245-165">En el menú de navegación de la parte superior, haga clic en **Configuration** (Configuración) y vaya a **Configure** (Configurar) en **Single Sign On** (Inicio de sesión único) para abrir la configuración del inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a3245-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="a3245-167">En el formulario **Single Sign On Settings** (Configuración de inicio de sesión), realice estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a3245-167">In **Single Sign On Settings** form perform the following steps:</span></span>
 
    <span data-ttu-id="a3245-168">a.</span><span class="sxs-lookup"><span data-stu-id="a3245-168">a.</span></span> <span data-ttu-id="a3245-169">Seleccione **Issuer Name** (Nombre del emisor) como Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3245-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="a3245-170">b.</span><span class="sxs-lookup"><span data-stu-id="a3245-170">b.</span></span> <span data-ttu-id="a3245-171">Pegue el **Identificador de entidad en SAML** que ha copiado de Azure Portal en el cuadro de texto Issuer URL (Dirección URL del emisor).</span><span class="sxs-lookup"><span data-stu-id="a3245-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="a3245-172">c.</span><span class="sxs-lookup"><span data-stu-id="a3245-172">c.</span></span> <span data-ttu-id="a3245-173">Copie la **Dirección URL de inicio de sesión único de SAML** que ha copiado de Azure Portal en el cuadro de texto Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="a3245-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="a3245-174">d.</span><span class="sxs-lookup"><span data-stu-id="a3245-174">d.</span></span> <span data-ttu-id="a3245-175">Pegue la **Dirección URL de cierre de sesión** que ha copiado de Azure Portal en el cuadro de texto Single Sign-Out Service URL (Dirección URL del servicio de cierre de sesión único).</span><span class="sxs-lookup"><span data-stu-id="a3245-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="a3245-176">e.</span><span class="sxs-lookup"><span data-stu-id="a3245-176">e.</span></span> <span data-ttu-id="a3245-177">Examine el certificado que ha descargado de Azure Portal y cárguelo aquí.</span><span class="sxs-lookup"><span data-stu-id="a3245-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="a3245-178">f.</span><span class="sxs-lookup"><span data-stu-id="a3245-178">f.</span></span> <span data-ttu-id="a3245-179">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a3245-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="a3245-180">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3245-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a3245-181">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a3245-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a3245-182">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a3245-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a3245-183">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3245-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="a3245-184">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a3245-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="a3245-186">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="a3245-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a3245-187">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3245-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a3245-189">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="a3245-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a3245-191">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a3245-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a3245-193">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="a3245-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a3245-195">a.</span><span class="sxs-lookup"><span data-stu-id="a3245-195">a.</span></span> <span data-ttu-id="a3245-196">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a3245-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a3245-197">b.</span><span class="sxs-lookup"><span data-stu-id="a3245-197">b.</span></span> <span data-ttu-id="a3245-198">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a3245-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a3245-199">c.</span><span class="sxs-lookup"><span data-stu-id="a3245-199">c.</span></span> <span data-ttu-id="a3245-200">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="a3245-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a3245-201">d.</span><span class="sxs-lookup"><span data-stu-id="a3245-201">d.</span></span> <span data-ttu-id="a3245-202">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="a3245-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="a3245-203">Creación de un usuario de prueba de SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="a3245-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="a3245-204">Para permitir que los usuarios de Azure AD se registren en SensoScientific Wireless Temperature Monitoring System, es necesario aprovisionarlos en dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3245-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="a3245-205">Colabore con el [equipo de soporte técnico de SensoScientific Wireless Temperature Monitoring System](https://www.sensoscientific.com/contact-us/) para agregar usuarios a la plataforma de SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="a3245-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="a3245-206">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="a3245-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a3245-207">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3245-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a3245-208">En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="a3245-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="a3245-210">**Para asignar a Britta Simon a SensoScientific Wireless Temperature Monitoring System, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="a3245-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="a3245-211">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="a3245-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="a3245-213">En la lista de aplicaciones, seleccione **SensoScientific Wireless Temperature Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="a3245-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="a3245-215">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a3245-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="a3245-217">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="a3245-217">Click **Add** button.</span></span> <span data-ttu-id="a3245-218">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a3245-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="a3245-220">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="a3245-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a3245-221">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="a3245-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a3245-222">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="a3245-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a3245-223">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="a3245-223">Testing single sign-on</span></span>

<span data-ttu-id="a3245-224">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="a3245-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="a3245-225">Haga clic en el icono de SensoScientific Wireless Temperature Monitoring System en el panel de acceso y después iniciará sesión automáticamente en dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="a3245-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="a3245-226">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a3245-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3245-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="a3245-227">Additional resources</span></span>

* [<span data-ttu-id="a3245-228">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3245-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a3245-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a3245-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

