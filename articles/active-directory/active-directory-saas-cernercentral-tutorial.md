---
title: "Tutorial: Integración de Azure Active Directory con Cerner Central | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="e0773-103">Tutorial: Integración de Azure Active Directory con Cerner Central</span><span class="sxs-lookup"><span data-stu-id="e0773-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="e0773-104">En este tutorial, obtendrá información sobre cómo integrar Cerner Central con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e0773-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e0773-105">Integrar Cerner Central con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e0773-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e0773-106">Puede controlar en Azure AD quién tiene acceso a Cerner Central</span><span class="sxs-lookup"><span data-stu-id="e0773-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="e0773-107">Puede permitir que los usuarios inicien sesión automáticamente en Cerner Central (inicio de sesión único) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0773-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e0773-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e0773-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e0773-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e0773-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0773-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e0773-110">Prerequisites</span></span>

<span data-ttu-id="e0773-111">Para configurar la integración de Azure AD con Cerner Central, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e0773-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="e0773-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0773-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e0773-113">Una cuenta de sistema de Cerner Central aprobada</span><span class="sxs-lookup"><span data-stu-id="e0773-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="e0773-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e0773-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e0773-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e0773-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e0773-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e0773-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e0773-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e0773-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e0773-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e0773-118">Scenario description</span></span>
<span data-ttu-id="e0773-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e0773-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e0773-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="e0773-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e0773-121">Agregar Cerner Central desde la galería</span><span class="sxs-lookup"><span data-stu-id="e0773-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="e0773-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0773-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="e0773-123">Agregar Cerner Central desde la galería</span><span class="sxs-lookup"><span data-stu-id="e0773-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="e0773-124">Para configurar la integración de Cerner Central en Azure AD, deberá agregar Cerner Central desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="e0773-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e0773-125">**Para agregar Cerner Central desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e0773-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e0773-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0773-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e0773-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e0773-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e0773-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e0773-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="e0773-131">Haga clic en el botón **Nueva aplicación** en la parte superior del cuadro de diálogo para agregar la nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0773-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="e0773-133">En el cuadro de búsqueda, escriba **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="e0773-133">In the search box, type **Cerner Central**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="e0773-135">En el panel de resultados, seleccione **Cerner Central** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0773-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e0773-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0773-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e0773-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Cerner Central con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e0773-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e0773-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Cerner Central para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0773-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="e0773-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="e0773-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="e0773-141">Para configurar y probar el inicio de sesión único de Azure AD con Cerner Central, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e0773-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e0773-142">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="e0773-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e0773-143">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0773-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e0773-144">**[Creación de un usuario de prueba de Cerner Central](#creating-a-cerner-central-test-user)**: para tener un homólogo de Britta Simon en Cerner Central que esté vinculado a la representación de Azure AD de usuario.</span><span class="sxs-lookup"><span data-stu-id="e0773-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="e0773-145">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e0773-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e0773-146">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e0773-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e0773-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0773-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e0773-148">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="e0773-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="e0773-149">**Para configurar el inicio de sesión único de Azure AD con Cerner Central, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e0773-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="e0773-150">En Azure Portal, en la página de integración de la aplicación **Cerner Central**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="e0773-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="e0773-152">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e0773-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="e0773-154">En la sección **Dominio y direcciones URL de Cerner Central**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0773-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="e0773-156">a.</span><span class="sxs-lookup"><span data-stu-id="e0773-156">a.</span></span> <span data-ttu-id="e0773-157">En el cuadro de texto **Identificador**, escriba el valor con los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="e0773-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="e0773-158">b.</span><span class="sxs-lookup"><span data-stu-id="e0773-158">b.</span></span> <span data-ttu-id="e0773-159">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="e0773-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="e0773-160">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="e0773-160">These values are not the real.</span></span> <span data-ttu-id="e0773-161">Actualice estos valores con el identificador y la URL de respuesta reales.</span><span class="sxs-lookup"><span data-stu-id="e0773-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e0773-162">Póngase en contacto con el [equipo de soporte técnico de Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="e0773-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="e0773-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="e0773-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="e0773-165">Para generar la dirección URL de **Metadatos**, lleve a cabo los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e0773-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="e0773-166">a.</span><span class="sxs-lookup"><span data-stu-id="e0773-166">a.</span></span> <span data-ttu-id="e0773-167">Haga clic en **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e0773-167">Click **App registrations**.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="e0773-169">b.</span><span class="sxs-lookup"><span data-stu-id="e0773-169">b.</span></span> <span data-ttu-id="e0773-170">Haga clic en **Puntos de conexión** para abrir el cuadro de diálogo **Puntos de conexión**.</span><span class="sxs-lookup"><span data-stu-id="e0773-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="e0773-172">c.</span><span class="sxs-lookup"><span data-stu-id="e0773-172">c.</span></span> <span data-ttu-id="e0773-173">Haga clic en el botón Copiar para copiar la dirección URL del **DOCUMENTO DE METADATOS DE FEDERACIÓN** y péguela en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="e0773-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="e0773-175">d.</span><span class="sxs-lookup"><span data-stu-id="e0773-175">d.</span></span> <span data-ttu-id="e0773-176">Ahora, vaya a la página de propiedades de **Cerner Central** y copie el **Id. de aplicación** con el botón **Copiar** y péguelo en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="e0773-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="e0773-178">e.</span><span class="sxs-lookup"><span data-stu-id="e0773-178">e.</span></span> <span data-ttu-id="e0773-179">Genere la **Dirección URL de metadatos** con el patrón siguiente: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="e0773-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="e0773-180">Para configurar el inicio de sesión único en el lado de **Cerner Central**, debe enviar la **Dirección URL de metadatos** al [equipo de soporte técnico de Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="e0773-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="e0773-181">El equipo se encargará de configurar el SSO en el lado de la aplicación para completar la integración.</span><span class="sxs-lookup"><span data-stu-id="e0773-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="e0773-182">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e0773-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e0773-183">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e0773-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e0773-184">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e0773-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e0773-185">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0773-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="e0773-186">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e0773-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="e0773-188">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="e0773-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e0773-189">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e0773-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e0773-191">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e0773-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e0773-193">Haga clic en **Agregar** para abrir el cuadro de diálogo **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="e0773-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e0773-195">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="e0773-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e0773-197">a.</span><span class="sxs-lookup"><span data-stu-id="e0773-197">a.</span></span> <span data-ttu-id="e0773-198">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e0773-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e0773-199">b.</span><span class="sxs-lookup"><span data-stu-id="e0773-199">b.</span></span> <span data-ttu-id="e0773-200">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e0773-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="e0773-201">c.</span><span class="sxs-lookup"><span data-stu-id="e0773-201">c.</span></span> <span data-ttu-id="e0773-202">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e0773-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e0773-203">d.</span><span class="sxs-lookup"><span data-stu-id="e0773-203">d.</span></span> <span data-ttu-id="e0773-204">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="e0773-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="e0773-205">Crear un usuario de prueba de Cerner Central</span><span class="sxs-lookup"><span data-stu-id="e0773-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="e0773-206">La aplicación **Cerner Central** permite la autenticación desde cualquier proveedor de identidades federado.</span><span class="sxs-lookup"><span data-stu-id="e0773-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="e0773-207">Si un usuario puede iniciar sesión en la página principal de la aplicación, significa que está federado y no necesita el aprovisionamiento manual.</span><span class="sxs-lookup"><span data-stu-id="e0773-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e0773-208">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e0773-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e0773-209">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="e0773-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="e0773-211">**Para asignar Britta Simon a Cerner Central, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="e0773-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="e0773-212">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="e0773-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="e0773-214">En la lista de aplicaciones, seleccione **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="e0773-214">In the applications list, select **Cerner Central**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="e0773-216">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e0773-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="e0773-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e0773-218">Click **Add** button.</span></span> <span data-ttu-id="e0773-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e0773-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="e0773-221">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="e0773-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e0773-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="e0773-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e0773-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e0773-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e0773-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e0773-224">Testing single sign-on</span></span>

<span data-ttu-id="e0773-225">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e0773-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e0773-226">Al hacer clic en el icono de Cerner Central en el Panel de acceso, debería iniciar sesión automáticamente en la aplicación Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="e0773-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="e0773-227">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e0773-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e0773-228">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e0773-228">Additional resources</span></span>

* [<span data-ttu-id="e0773-229">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0773-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e0773-230">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e0773-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

