---
title: "Tutorial: integración de Azure Active Directory con Wdesk | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="2565d-103">Tutorial: integración de Azure Active Directory con Wdesk</span><span class="sxs-lookup"><span data-stu-id="2565d-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="2565d-104">En este tutorial, aprenderá a integrar Wdesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2565d-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2565d-105">La integración de Wdesk con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2565d-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2565d-106">Puede controlar en Azure AD quién tiene acceso a Wdesk</span><span class="sxs-lookup"><span data-stu-id="2565d-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="2565d-107">Puede permitir que los usuarios inicien sesión automáticamente en Wdesk (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2565d-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2565d-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2565d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2565d-109">Si quiere conocer más detalles sobre la integración de aplicaciones SaaS con Azure AD, vea:</span><span class="sxs-lookup"><span data-stu-id="2565d-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="2565d-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="2565d-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2565d-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2565d-111">Prerequisites</span></span>

<span data-ttu-id="2565d-112">Para configurar la integración de Azure AD con Wdesk, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2565d-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="2565d-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2565d-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2565d-114">Una suscripción habilitada para el inicio de sesión único en Wdesk</span><span class="sxs-lookup"><span data-stu-id="2565d-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2565d-115">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2565d-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2565d-116">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2565d-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2565d-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2565d-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2565d-118">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2565d-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2565d-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2565d-119">Scenario description</span></span>
<span data-ttu-id="2565d-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2565d-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2565d-121">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="2565d-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2565d-122">Adición de Wdesk desde la galería</span><span class="sxs-lookup"><span data-stu-id="2565d-122">Adding Wdesk from the gallery</span></span>
2. <span data-ttu-id="2565d-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2565d-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="2565d-124">Adición de Wdesk desde la galería</span><span class="sxs-lookup"><span data-stu-id="2565d-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="2565d-125">Para configurar la integración de Wdesk en Azure AD, es preciso agregar Wdesk desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="2565d-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2565d-126">**Para agregar Wdesk desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2565d-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2565d-127">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2565d-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2565d-129">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2565d-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2565d-130">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2565d-130">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2565d-132">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2565d-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2565d-134">En el cuadro de búsqueda, escriba **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="2565d-134">In the search box, type **Wdesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="2565d-136">En el panel de resultados, seleccione **Wdesk** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2565d-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2565d-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2565d-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2565d-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Wdesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2565d-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2565d-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Wdesk para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2565d-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="2565d-141">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2565d-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="2565d-142">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2565d-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="2565d-143">Para configurar y probar el inicio de sesión único de Azure AD con Wdesk, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2565d-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2565d-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="2565d-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2565d-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2565d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2565d-146">**[Creación de un usuario de prueba de Wdesk](#creating-a-wdesk-test-user)**: el objetivo es tener un homólogo de Britta Simon en Wdesk que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2565d-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2565d-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2565d-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2565d-148">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2565d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2565d-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2565d-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2565d-150">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2565d-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="2565d-151">**Para configurar el inicio de sesión único de Azure AD con Wdesk, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2565d-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2565d-152">En Azure Portal, en la página de integración de la aplicación **Wdesk**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2565d-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2565d-154">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2565d-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="2565d-156">En la sección **Dominio y direcciones URL de Wdesk**, si quiere configurar la aplicación en el modo iniciado por **IDP**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2565d-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="2565d-158">a.</span><span class="sxs-lookup"><span data-stu-id="2565d-158">a.</span></span> <span data-ttu-id="2565d-159">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2565d-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="2565d-160">b.</span><span class="sxs-lookup"><span data-stu-id="2565d-160">b.</span></span> <span data-ttu-id="2565d-161">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="2565d-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="2565d-162">Active **Mostrar configuración avanzada de URL**.</span><span class="sxs-lookup"><span data-stu-id="2565d-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2565d-163">Si desea configurar la aplicación en modo iniciado por **SP**, realice el siguientes paso:</span><span class="sxs-lookup"><span data-stu-id="2565d-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="2565d-165">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="2565d-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2565d-166">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2565d-166">These values are not real.</span></span> <span data-ttu-id="2565d-167">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="2565d-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2565d-168">Estos valores se obtienen de portal de WDesk al configurar el SSO.</span><span class="sxs-lookup"><span data-stu-id="2565d-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
5. <span data-ttu-id="2565d-169">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2565d-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="2565d-171">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2565d-171">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="2565d-173">En otra ventana del explorador web, inicie sesión en Wdesk como Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="2565d-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="2565d-174">En la parte inferior izquierda, haga clic en **Admin** (Administración) y elija **Account Admin** (Administrador de cuenta):</span><span class="sxs-lookup"><span data-stu-id="2565d-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="2565d-176">En Wdesk Admin, navegue hasta **Security** (Seguridad) y, después, **SAML** > **SAML Settings** (Configuración de SAML):</span><span class="sxs-lookup"><span data-stu-id="2565d-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="2565d-178">En **General Settings** (Configuración general), seleccione la casilla **Enable SAML Single Sign On** (Habilitar inicio de sesión único de SAML):</span><span class="sxs-lookup"><span data-stu-id="2565d-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="2565d-180">En **Service Provider Details** (Detalles del proveedor de servicios), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="2565d-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="2565d-182">a.</span><span class="sxs-lookup"><span data-stu-id="2565d-182">a.</span></span> <span data-ttu-id="2565d-183">Copia el valor de **Login URL** (Dirección URL de inicio de sesión) y péguelo en el cuadro de texto **Dirección URL de inicio de sesión** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2565d-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="2565d-184">b.</span><span class="sxs-lookup"><span data-stu-id="2565d-184">b.</span></span> <span data-ttu-id="2565d-185">Copia el valor de **Metadata Url** (Dirección URL de metadatos) y péguelo en el cuadro de texto **Identificador** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2565d-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="2565d-186">c.</span><span class="sxs-lookup"><span data-stu-id="2565d-186">c.</span></span> <span data-ttu-id="2565d-187">Copia el valor de **Consumer url** (Dirección URL del consumidor ) y péguelo en el cuadro de texto **URL de respuesta** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2565d-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="2565d-188">d.</span><span class="sxs-lookup"><span data-stu-id="2565d-188">d.</span></span> <span data-ttu-id="2565d-189">Haga clic en **Guardar** en Azure Portal para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="2565d-189">Click **Save** on Azure portal to save the changes.</span></span>      

12. <span data-ttu-id="2565d-190">Haga clic en **Configure IdP Settings** (Configurar valores de IdP) para abrir el cuadro de diálogo **Edit IdP Settings** (Editar valores de IdP).</span><span class="sxs-lookup"><span data-stu-id="2565d-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="2565d-191">Haga clic en **Choose File** (Elegir archivo) para buscar el archivo **Metadata.xml** que guardó en Azure Portal y cárguelo.</span><span class="sxs-lookup"><span data-stu-id="2565d-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="2565d-193">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="2565d-193">Click **Save changes**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="2565d-195">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2565d-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2565d-196">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="2565d-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2565d-197">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2565d-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2565d-198">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2565d-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="2565d-199">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2565d-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2565d-201">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="2565d-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2565d-202">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2565d-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2565d-204">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2565d-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2565d-206">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2565d-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2565d-208">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2565d-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2565d-210">a.</span><span class="sxs-lookup"><span data-stu-id="2565d-210">a.</span></span> <span data-ttu-id="2565d-211">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2565d-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2565d-212">b.</span><span class="sxs-lookup"><span data-stu-id="2565d-212">b.</span></span> <span data-ttu-id="2565d-213">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2565d-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2565d-214">c.</span><span class="sxs-lookup"><span data-stu-id="2565d-214">c.</span></span> <span data-ttu-id="2565d-215">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2565d-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2565d-216">d.</span><span class="sxs-lookup"><span data-stu-id="2565d-216">d.</span></span> <span data-ttu-id="2565d-217">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2565d-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="2565d-218">Creación de usuario de prueba de Wdesk</span><span class="sxs-lookup"><span data-stu-id="2565d-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="2565d-219">Para permitir que los usuarios de Azure AD inicien sesión en Wdesk, tienen que aprovisionarse en Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2565d-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="2565d-220">En el caso de Wdesk, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2565d-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="2565d-221">**Para aprovisionar una cuenta de usuario, realice estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2565d-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2565d-222">Inicie sesión en Wdesk como administrador de seguridad.</span><span class="sxs-lookup"><span data-stu-id="2565d-222">Log in to Wdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="2565d-223">Navegue hasta **Admin** (Administración)  > **Account Admin** (Administrador de cuenta).</span><span class="sxs-lookup"><span data-stu-id="2565d-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="2565d-225">Haga clic en **Members** (Miembros) en **People** (Contactos).</span><span class="sxs-lookup"><span data-stu-id="2565d-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="2565d-226">A continuación, haga clic en **Add Member** (Agregar miembro) para abrir el cuadro de diálogo **(Agregar miembro)**.</span><span class="sxs-lookup"><span data-stu-id="2565d-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="2565d-228">En el cuadro de texto **User** (Usuario), escriba el nombre del usuario así **brittasimon@contoso.com** y haga clic en el botón **Continue** (Continuar).</span><span class="sxs-lookup"><span data-stu-id="2565d-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="2565d-230">Escriba los detalles que se muestran a continuación:</span><span class="sxs-lookup"><span data-stu-id="2565d-230">Enter the details as shown below:</span></span>
  
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="2565d-232">a.</span><span class="sxs-lookup"><span data-stu-id="2565d-232">a.</span></span> <span data-ttu-id="2565d-233">En el cuadro de texto **E-mail** (Correo electrónico), escriba el correo electrónico del usuario con el siguiente formato **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2565d-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2565d-234">b.</span><span class="sxs-lookup"><span data-stu-id="2565d-234">b.</span></span> <span data-ttu-id="2565d-235">En el cuadro de texto **First Name** (Nombre), escriba el nombre de usuario, en este caso **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2565d-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="2565d-236">c.</span><span class="sxs-lookup"><span data-stu-id="2565d-236">c.</span></span> <span data-ttu-id="2565d-237">En el cuadro de texto **Last Name** (Apellidos), escriba el nombre de usuario, en este caso **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2565d-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

7. <span data-ttu-id="2565d-238">Haga clic en el botón **Save Member** (Guardar miembro).</span><span class="sxs-lookup"><span data-stu-id="2565d-238">Click **Save Member** button.</span></span>  

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2565d-240">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2565d-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2565d-241">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2565d-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2565d-243">**Para asignar Britta Simon a Wdesk, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="2565d-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2565d-244">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2565d-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2565d-246">En la lista de aplicaciones, seleccione **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="2565d-246">In the applications list, select **Wdesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="2565d-248">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2565d-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2565d-250">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2565d-250">Click **Add** button.</span></span> <span data-ttu-id="2565d-251">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2565d-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2565d-253">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="2565d-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2565d-254">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2565d-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2565d-255">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2565d-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2565d-256">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2565d-256">Testing single sign-on</span></span>

<span data-ttu-id="2565d-257">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2565d-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2565d-258">Al hacer clic en el icono de Wdesk en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2565d-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="2565d-259">Para más información sobre el Panel de acceso, vea la [introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2565d-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2565d-260">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2565d-260">Additional resources</span></span>

* [<span data-ttu-id="2565d-261">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2565d-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2565d-262">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2565d-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

