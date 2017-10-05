---
title: "Tutorial: Integración de Azure Active Directory con Proofpoint on Demand | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Proofpoint on Demand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: b4c8d8c187fc865a905016f04a41843894249f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="fd85b-103">Tutorial: Integración de Azure Active Directory con Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="fd85b-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="fd85b-104">En este tutorial, aprenderá a integrar Proofpoint on Demand con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd85b-104">In this tutorial, you learn how to integrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd85b-105">La integración de Proofpoint on Demand con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fd85b-105">Integrating Proofpoint on Demand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fd85b-106">Puede controlar en Azure AD quién tiene acceso a Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-106">You can control in Azure AD who has access to Proofpoint on Demand</span></span>
- <span data-ttu-id="fd85b-107">Puede permitir que los usuarios inicien sesión automáticamente en Proofpoint on Demand (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd85b-107">You can enable your users to automatically get signed-on to Proofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fd85b-108">Puede administrar las cuentas en una sola ubicación central: Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fd85b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fd85b-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fd85b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd85b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fd85b-110">Prerequisites</span></span>

<span data-ttu-id="fd85b-111">Para configurar la integración de Azure AD con Proofpoint on Demand, se necesitan los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fd85b-111">To configure Azure AD integration with Proofpoint on Demand, you need the following items:</span></span>

- <span data-ttu-id="fd85b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd85b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fd85b-113">Una suscripción habilitada para el inicio de sesión único en Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="fd85b-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd85b-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fd85b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fd85b-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fd85b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fd85b-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fd85b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd85b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd85b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd85b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fd85b-118">Scenario description</span></span>
<span data-ttu-id="fd85b-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fd85b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fd85b-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="fd85b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fd85b-121">Adición de Proofpoint on Demand desde la galería</span><span class="sxs-lookup"><span data-stu-id="fd85b-121">Adding Proofpoint on Demand from the gallery</span></span>
2. <span data-ttu-id="fd85b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd85b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-the-gallery"></a><span data-ttu-id="fd85b-123">Adición de Proofpoint on Demand desde la galería</span><span class="sxs-lookup"><span data-stu-id="fd85b-123">Adding Proofpoint on Demand from the gallery</span></span>
<span data-ttu-id="fd85b-124">Para configurar la integración de Proofpoint on Demand en Azure AD, deberá agregar Proofpoint on Demand desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="fd85b-124">To configure the integration of Proofpoint on Demand into Azure AD, you need to add Proofpoint on Demand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fd85b-125">**Para agregar Proofpoint on Demand desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fd85b-125">**To add Proofpoint on Demand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fd85b-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fd85b-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fd85b-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="fd85b-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fd85b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="fd85b-133">En el cuadro de búsqueda, escriba **Proofpoint in Demand**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-133">In the search box, type **Proofpoint on Demand**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="fd85b-135">En el panel de resultados, seleccione **Proofpoint on Demand** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd85b-135">In the results panel, select **Proofpoint on Demand**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fd85b-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd85b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fd85b-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Proofpoint on Demand con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fd85b-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fd85b-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Proofpoint on Demand para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd85b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Proofpoint on Demand is to a user in Azure AD.</span></span> <span data-ttu-id="fd85b-140">Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-140">In other words, a link relationship between an Azure AD user and the related user in Proofpoint on Demand needs to be established.</span></span>

<span data-ttu-id="fd85b-141">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="fd85b-142">Para configurar y probar el inicio de sesión único de Azure AD con Proofpoint on Demand, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fd85b-142">To configure and test Azure AD single sign-on with Proofpoint on Demand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fd85b-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="fd85b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fd85b-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd85b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fd85b-145">**[Creación de un usuario de prueba de Proofpoint on Demand](#creating-a-proofpoint-on-demand-test-user)**: el objetivo es tener un homólogo de Britta Simon en Proofpoint on Demand que esté vinculado a la representación del usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd85b-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - to have a counterpart of Britta Simon in Proofpoint on Demand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fd85b-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd85b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fd85b-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fd85b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fd85b-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd85b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fd85b-149">En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="fd85b-150">**Para configurar el inicio de sesión único de Azure AD con Proofpoint on Demand, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fd85b-150">**To configure Azure AD single sign-on with Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="fd85b-151">En la página de integración de la aplicación **Proofpoint on Demand** de Azure Portal, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-151">In the Azure portal, on the **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="fd85b-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fd85b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
  
    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="fd85b-155">En la sección **Dominio y direcciones URL de Proofpoint on Demand**, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="fd85b-155">On the **Proofpoint on Demand Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="fd85b-157">En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<hostname>.pphosted.com/ppssamlsp_hostname`.</span><span class="sxs-lookup"><span data-stu-id="fd85b-157">a.In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="fd85b-158">b.</span><span class="sxs-lookup"><span data-stu-id="fd85b-158">b.</span></span> <span data-ttu-id="fd85b-159">En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="fd85b-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="fd85b-160">c.</span><span class="sxs-lookup"><span data-stu-id="fd85b-160">c.</span></span>  <span data-ttu-id="fd85b-161">En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`.</span><span class="sxs-lookup"><span data-stu-id="fd85b-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="fd85b-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="fd85b-162">These values are not the real.</span></span> <span data-ttu-id="fd85b-163">Actualice estos valores con los valores reales de Identificador, URL de respuesta y URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="fd85b-163">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="fd85b-164">Póngase en contacto con el [equipo de soporte técnico de Proofpoint on Demand](https://www.proofpoint.com/us/support-services) para obtener estos valores.</span><span class="sxs-lookup"><span data-stu-id="fd85b-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to get these values.</span></span> 

4. <span data-ttu-id="fd85b-165">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fd85b-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="fd85b-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fd85b-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="fd85b-169">En la sección **Configuración de Proofpoint on Demand**, haga clic en **Configurar Proofpoint on Demand** para abrir la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-169">On the **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fd85b-170">Copie los valores de **SAML Entity ID y SAML Single Sign-On Service URL** (Identificador de entidad de SAML y URL del servicio de inicio de sesión único de SAML) de la sección de **referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-170">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="fd85b-172">Para configurar el inicio de sesión único en **Proofpoint on Demand**, es preciso enviar el **certificado (Base64)** descargado, el **id. de entidad de SAML** y la **dirección URL del servicio de inicio de sesión único de SAML** al [equipo de atención al cliente de Proofpoint on Demand](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="fd85b-172">To configure single sign-on on **Proofpoint on Demand** side, you need to send the downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="fd85b-173">Ahora puede leer una versión concisa de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fd85b-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fd85b-174">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="fd85b-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fd85b-175">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fd85b-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fd85b-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd85b-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="fd85b-177">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fd85b-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="fd85b-179">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="fd85b-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fd85b-180">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd85b-182">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="fd85b-182">These values are not the real.</span></span> <span data-ttu-id="fd85b-183">Actualícelos con los datos reales.</span><span class="sxs-lookup"><span data-stu-id="fd85b-183">Update these values with the actual</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fd85b-185">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fd85b-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd85b-187">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="fd85b-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd85b-189">a.</span><span class="sxs-lookup"><span data-stu-id="fd85b-189">a.</span></span> <span data-ttu-id="fd85b-190">En el cuadro de texto **Nombre**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-190">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="fd85b-191">b.</span><span class="sxs-lookup"><span data-stu-id="fd85b-191">b.</span></span> <span data-ttu-id="fd85b-192">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd85b-192">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="fd85b-193">c.</span><span class="sxs-lookup"><span data-stu-id="fd85b-193">c.</span></span> <span data-ttu-id="fd85b-194">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fd85b-195">d.</span><span class="sxs-lookup"><span data-stu-id="fd85b-195">d.</span></span> <span data-ttu-id="fd85b-196">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="fd85b-197">Creación de un usuario de prueba de Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="fd85b-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="fd85b-198">En esta sección, creará un usuario llamado Britta Simon en Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="fd85b-199">Trabaje con el [equipo de atención al cliente de Proofpoint on Demand](https://www.proofpoint.com/us/support-services) para agregar usuarios a la plataforma Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) to add users in the Proofpoint on Demand platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fd85b-200">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd85b-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fd85b-201">En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Proofpoint on Demand.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="fd85b-203">**Para asignar a Britta Simon a Proofpoint on Demand, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="fd85b-203">**To assign Britta Simon to Proofpoint on Demand, perform the following steps:**</span></span>

1. <span data-ttu-id="fd85b-204">En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fd85b-206">En la lista de aplicaciones, seleccione **Proofpoint on Demand**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-206">In the applications list, select **Proofpoint on Demand**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="fd85b-208">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="fd85b-210">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-210">Click **Add** button.</span></span> <span data-ttu-id="fd85b-211">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="fd85b-213">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="fd85b-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fd85b-214">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fd85b-215">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fd85b-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fd85b-216">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="fd85b-216">Testing single sign-on</span></span>

<span data-ttu-id="fd85b-217">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fd85b-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fd85b-218">Al hacer clic en el icono **Proofpoint on Demand** del Panel de acceso, debería iniciar sesión automáticamente en su aplicación Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="fd85b-218">When you click the **Proofpoint on Demand** tile on the Access Panel, you should be automatically signed on to your Proofpoint on Demand application.</span></span>
<span data-ttu-id="fd85b-219">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fd85b-219">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="fd85b-220">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fd85b-220">Additional resources</span></span>

* [<span data-ttu-id="fd85b-221">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd85b-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd85b-222">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fd85b-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

