---
title: "Tutorial: integración de Azure Active Directory con FreshGrade | Microsoft Azure"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 3ff3e5aab679f8ee610c98f8a4089308adcce48f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="f5a4f-103">Tutorial: integración de Azure Active Directory con FreshGrade</span><span class="sxs-lookup"><span data-stu-id="f5a4f-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="f5a4f-104">En este tutorial, aprenderá cómo integrar FreshGrade con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5a4f-104">In this tutorial, you learn how to integrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5a4f-105">La integración de FreshGrade con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-105">Integrating FreshGrade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5a4f-106">Puede controlar en Azure AD quién tiene acceso a FreshGrade</span><span class="sxs-lookup"><span data-stu-id="f5a4f-106">You can control in Azure AD who has access to FreshGrade</span></span>
- <span data-ttu-id="f5a4f-107">Puede permitir que los usuarios inicien sesión automáticamente en FreshGrade (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a4f-107">You can enable your users to automatically get signed-on to FreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5a4f-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5a4f-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f5a4f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5a4f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f5a4f-110">Prerequisites</span></span>

<span data-ttu-id="f5a4f-111">Para configurar la integración de Azure AD con FreshGrade, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-111">To configure Azure AD integration with FreshGrade, you need the following items:</span></span>

- <span data-ttu-id="f5a4f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5a4f-113">Una suscripción habilitada para inicio de sesión único en FreshGrade</span><span class="sxs-lookup"><span data-stu-id="f5a4f-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5a4f-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5a4f-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5a4f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5a4f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5a4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5a4f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="f5a4f-118">Scenario description</span></span>
<span data-ttu-id="f5a4f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5a4f-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5a4f-121">Incorporación de FreshGrade desde la galería</span><span class="sxs-lookup"><span data-stu-id="f5a4f-121">Adding FreshGrade from the gallery</span></span>
2. <span data-ttu-id="f5a4f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-the-gallery"></a><span data-ttu-id="f5a4f-123">Incorporación de FreshGrade desde la galería</span><span class="sxs-lookup"><span data-stu-id="f5a4f-123">Adding FreshGrade from the gallery</span></span>
<span data-ttu-id="f5a4f-124">Para configurar la integración de FreshGrade en Azure AD, deberá agregar FreshGrade desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-124">To configure the integration of FreshGrade into Azure AD, you need to add FreshGrade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5a4f-125">**Para agregar FreshGrade desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="f5a4f-125">**To add FreshGrade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5a4f-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5a4f-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5a4f-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="f5a4f-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="f5a4f-133">En el cuadro de búsqueda, escriba **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-133">In the search box, type **FreshGrade**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="f5a4f-135">En el panel de resultados, seleccione **FreshGrade** y luego haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-135">In the results panel, select **FreshGrade**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5a4f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a4f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5a4f-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con FreshGrade con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5a4f-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5a4f-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de FreshGrade para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshGrade is to a user in Azure AD.</span></span> <span data-ttu-id="f5a4f-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-140">In other words, a link relationship between an Azure AD user and the related user in FreshGrade needs to be established.</span></span>

<span data-ttu-id="f5a4f-141">Para establecer la relación de vínculo en FreshGrade, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-141">In FreshGrade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5a4f-142">Para configurar y probar el inicio de sesión único de Azure AD con FreshGrade, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-142">To configure and test Azure AD single sign-on with FreshGrade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5a4f-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5a4f-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5a4f-145">**[Creación de un usuario de prueba de FreshGrade](#creating-a-freshgrade-test-user)**: para tener un homólogo de Britta Simon en FreshGrade que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - to have a counterpart of Britta Simon in FreshGrade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5a4f-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5a4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5a4f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a4f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5a4f-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="f5a4f-150">**Para configurar el inicio de sesión único de Azure AD con FreshGrade, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f5a4f-150">**To configure Azure AD single sign-on with FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="f5a4f-151">En Azure Portal, en la página de integración de la aplicación **FreshGrade**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-151">In the Azure portal, on the **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="f5a4f-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="f5a4f-155">En la sección **Dominio y direcciones URL de FreshGrade**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-155">On the **FreshGrade Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="f5a4f-157">a.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-157">a.</span></span> <span data-ttu-id="f5a4f-158">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="f5a4f-159">b.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-159">b.</span></span> <span data-ttu-id="f5a4f-160">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="f5a4f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-161">These values are not real.</span></span> <span data-ttu-id="f5a4f-162">Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5a4f-163">Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de clientes de FreshGrade](mailTo:support@freshgrade.com) .</span><span class="sxs-lookup"><span data-stu-id="f5a4f-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) to get these values.</span></span> 
 


4. <span data-ttu-id="f5a4f-164">En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="f5a4f-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="f5a4f-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5a4f-168">En la sección **Configuración de FreshGrade**, haga clic en **Configurar FreshGrade** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-168">On the **FreshGrade Configuration** section, click **Configure FreshGrade** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f5a4f-169">Copie la **dirección URL de servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="f5a4f-171">Para generar la dirección URL de **Metadatos**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-171">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="f5a4f-172">a.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-172">a.</span></span> <span data-ttu-id="f5a4f-173">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-173">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="f5a4f-175">b.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-175">b.</span></span> <span data-ttu-id="f5a4f-176">Haga clic en **Puntos de conexión** para abrir el cuadro de diálogo **Puntos de conexión**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-176">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="f5a4f-178">c.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-178">c.</span></span> <span data-ttu-id="f5a4f-179">Haga clic en el botón Copiar para copiar la dirección URL del **DOCUMENTO DE METADATOS DE FEDERACIÓN** y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-179">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="f5a4f-181">d.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-181">d.</span></span> <span data-ttu-id="f5a4f-182">Ahora, vaya a la página de propiedades de **FreshGrade** y copie el **Id. de aplicación** con el botón **Copiar** y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-182">Now go to the property page of **FreshGrade** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="f5a4f-184">e.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-184">e.</span></span> <span data-ttu-id="f5a4f-185">Genere la **Dirección URL de metadatos** con el patrón siguiente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="f5a4f-185">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="f5a4f-186">Para configurar el inicio de sesión único en **FreshGrade**, es preciso enviar la **Dirección URL de metadatos** y la **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) al [equipo de soporte técnico de FreshGrade](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="f5a4f-186">To configure single sign-on on **FreshGrade** side, you need to send the **Metadata URL** and **SAML Single Sign-On Service URL** to [FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="f5a4f-187">Dicho equipo lo configura para establecer la conexión de SSO de SAML correctamente en ambos lados.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f5a4f-188">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5a4f-189">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5a4f-190">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5a4f-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5a4f-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a4f-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5a4f-192">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5a4f-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="f5a4f-194">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="f5a4f-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5a4f-195">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5a4f-197">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5a4f-199">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5a4f-201">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="f5a4f-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5a4f-203">a.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-203">a.</span></span> <span data-ttu-id="f5a4f-204">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5a4f-205">b.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-205">b.</span></span> <span data-ttu-id="f5a4f-206">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5a4f-207">c.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-207">c.</span></span> <span data-ttu-id="f5a4f-208">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5a4f-209">d.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-209">d.</span></span> <span data-ttu-id="f5a4f-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="f5a4f-211">Creación de un usuario de prueba FreshGrade</span><span class="sxs-lookup"><span data-stu-id="f5a4f-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="f5a4f-212">En esta sección, creará un usuario llamado Britta Simon en FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="f5a4f-213">Trabaje con el [equipo de soporte técnico de FreshGrade](mailTo:support@freshgrade.com) para agregar los usuarios a la plataforma de FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) to add the users in the FreshGrade platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5a4f-214">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="f5a4f-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5a4f-215">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FreshGrade.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="f5a4f-217">**Para asignar a Britta Simon a FreshGrade, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="f5a4f-217">**To assign Britta Simon to FreshGrade, perform the following steps:**</span></span>

1. <span data-ttu-id="f5a4f-218">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="f5a4f-220">En la lista de aplicaciones, seleccione **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-220">In the applications list, select **FreshGrade**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="f5a4f-222">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="f5a4f-224">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-224">Click **Add** button.</span></span> <span data-ttu-id="f5a4f-225">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="f5a4f-227">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5a4f-228">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5a4f-229">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5a4f-230">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="f5a4f-230">Testing single sign-on</span></span>

<span data-ttu-id="f5a4f-231">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f5a4f-232">Al hacer clic en el icono de FreshGrade en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="f5a4f-232">When you click the FreshGrade tile in the Access Panel, you should get automatically signed-on to your FreshGrade application.</span></span>
<span data-ttu-id="f5a4f-233">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f5a4f-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5a4f-234">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="f5a4f-234">Additional resources</span></span>

* [<span data-ttu-id="f5a4f-235">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5a4f-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5a4f-236">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f5a4f-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

