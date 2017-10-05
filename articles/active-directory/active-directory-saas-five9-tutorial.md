---
title: "Tutorial: integración de Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs"
description: "Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Five9 Plus Adapter (CTI, Contact Center Agents)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: d75163ea5eb3fa811e07861f06e6c4d5c758b898
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="b28cb-103">Tutorial: integración de Azure Active Directory con Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="b28cb-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="b28cb-104">En este tutorial aprenderá a integrar Five9 Plus Adapter (CTI, Contact Center Agents) con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b28cb-104">In this tutorial, you learn how to integrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b28cb-105">La integración de Five9 Plus Adapter (CTI, Contact Center Agents) con Azure AD le proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b28cb-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b28cb-106">Puede controlar en Azure AD quién tiene acceso a Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="b28cb-106">You can control in Azure AD who has access to Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="b28cb-107">Puede permitir que los usuarios inicien sesión automáticamente en Five9 Plus Adapter (CTI, Contact Center Agents) (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b28cb-107">You can enable your users to automatically get signed-on to Five9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b28cb-108">Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b28cb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b28cb-109">Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b28cb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b28cb-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b28cb-110">Prerequisites</span></span>

<span data-ttu-id="b28cb-111">Para configurar la integración de Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents), necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b28cb-111">To configure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need the following items:</span></span>

- <span data-ttu-id="b28cb-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b28cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b28cb-113">Una suscripción habilitada para el inicio de sesión único de Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="b28cb-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b28cb-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b28cb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b28cb-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b28cb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b28cb-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b28cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b28cb-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b28cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b28cb-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b28cb-118">Scenario description</span></span>
<span data-ttu-id="b28cb-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b28cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b28cb-120">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="b28cb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b28cb-121">Agregar Five9 Plus Adapter (CTI, Contact Center Agents) desde la galería</span><span class="sxs-lookup"><span data-stu-id="b28cb-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
2. <span data-ttu-id="b28cb-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b28cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-the-gallery"></a><span data-ttu-id="b28cb-123">Agregar Five9 Plus Adapter (CTI, Contact Center Agents) desde la galería</span><span class="sxs-lookup"><span data-stu-id="b28cb-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
<span data-ttu-id="b28cb-124">Para configurar la integración de Five9 Plus Adapter (CTI, Contact Center Agents) en Azure AD, deberá agregar Five9 Plus Adapter (CTI, Contact Center Agents) desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="b28cb-124">To configure the integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need to add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b28cb-125">**Para agregar Five9 Plus Adapter (CTI, Contact Center Agents) desde la galería, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="b28cb-125">**To add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b28cb-126">En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b28cb-128">Vaya a **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b28cb-129">A continuación, vaya a **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-129">Then go to **All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b28cb-131">Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b28cb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b28cb-133">En el cuadro de búsqueda, escriba **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-133">In the search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. <span data-ttu-id="b28cb-135">En el panel de resultados, seleccione **Five9 Plus Adapter (CTI, Contact Center Agents)** y haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b28cb-135">In the results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button to add the application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b28cb-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b28cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b28cb-138">En esta sección puede configurar y probar el inicio de sesión único de Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents) con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b28cb-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b28cb-139">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Five9 Plus Adapter (CTI, Contact Center Agents) para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b28cb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is to a user in Azure AD.</span></span> <span data-ttu-id="b28cb-140">Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="b28cb-140">In other words, a link relationship between an Azure AD user and the related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs to be established.</span></span>

<span data-ttu-id="b28cb-141">Para establecer la relación de vínculo, en Five9 Plus Adapter (CTI, Contact Center Agents), asigne el valor del **nombre de usuario** de Azure AD como valor del **nombre de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b28cb-142">Para configurar y probar el inicio de sesión único de Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents), es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b28cb-142">To configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b28cb-143">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b28cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b28cb-144">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b28cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b28cb-145">**[Creación de un usuario de prueba de Five9 Plus Adapter (CTI, Contact Center Agents)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**: para disponer de un usuario homólogo de Britta Simon en Five9 Plus Adapter (CTI, Contact Center Agents) que esté vinculado a la representación de Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b28cb-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - to have a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b28cb-146">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b28cb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b28cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b28cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b28cb-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b28cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b28cb-149">En esta sección habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="b28cb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="b28cb-150">**Para configurar el inicio de sesión único de Azure AD con Five9 Plus Adapter (CTI, Contact Center Agents), lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="b28cb-150">**To configure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="b28cb-151">En Azure Portal, en la página de integración de la aplicación **Five9 Plus Adapter (CTI, Contact Center Agents)**, haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-151">In the Azure portal, on the **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b28cb-153">En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b28cb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. <span data-ttu-id="b28cb-155">En la sección **Dominio y direcciones URL de Five9 Plus Adapter (CTI, Contact Center Agents)**, lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b28cb-155">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform the following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="b28cb-157">a.</span><span class="sxs-lookup"><span data-stu-id="b28cb-157">a.</span></span> <span data-ttu-id="b28cb-158">En el cuadro de texto **Identificador**, escriba una dirección URL con los siguientes patrones:</span><span class="sxs-lookup"><span data-stu-id="b28cb-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span>

    |    <span data-ttu-id="b28cb-159">Environment</span><span class="sxs-lookup"><span data-stu-id="b28cb-159">Environment</span></span>      |       <span data-ttu-id="b28cb-160">URL</span><span class="sxs-lookup"><span data-stu-id="b28cb-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="b28cb-161">Para "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="b28cb-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="b28cb-162">Para "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="b28cb-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="b28cb-163">Para "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="b28cb-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="b28cb-164">b.</span><span class="sxs-lookup"><span data-stu-id="b28cb-164">b.</span></span> <span data-ttu-id="b28cb-165">En el cuadro de texto **URL de respuesta** , escriba una dirección URL con el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="b28cb-165">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    |      <span data-ttu-id="b28cb-166">Environment</span><span class="sxs-lookup"><span data-stu-id="b28cb-166">Environment</span></span>     |      <span data-ttu-id="b28cb-167">URL</span><span class="sxs-lookup"><span data-stu-id="b28cb-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="b28cb-168">Para "Five9 Plus Adapter for Microsoft Dynamics CRM"</span><span class="sxs-lookup"><span data-stu-id="b28cb-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="b28cb-169">Para "Five9 Plus Adapter for Zendesk"</span><span class="sxs-lookup"><span data-stu-id="b28cb-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="b28cb-170">Para "Five9 Plus Adapter for Agent Desktop Toolkit"</span><span class="sxs-lookup"><span data-stu-id="b28cb-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. <span data-ttu-id="b28cb-171">En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b28cb-171">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. <span data-ttu-id="b28cb-173">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b28cb-173">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b28cb-175">En la sección **Configuración de Five9 Plus Adapter (CTI, Contact Center Agents)**, haga clic en **Configurar Five9 Plus Adapter (CTI, Contact Center Agents)** para que se abra la ventana **Configurar inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-175">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b28cb-176">Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. <span data-ttu-id="b28cb-178">Para configurar el inicio de sesión único en **Five9 Plus Adapter (CTI, Contact Center Agents)**, debe enviar el **certificado descargado (Base64), la dirección URL de cierre de sesión, el identificador de entidad de SAML y la dirección URL del servicio de inicio de sesión único de SAML** al [equipo de soporte técnico de Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="b28cb-178">To configure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="b28cb-179">Además, para configurar aún más el inicio de sesión único, puede seguir los pasos descritos a continuación en función del adaptador:</span><span class="sxs-lookup"><span data-stu-id="b28cb-179">Also additionally, for configuring SSO further please follow the below steps according to the adapter:</span></span>

    <span data-ttu-id="b28cb-180">a.</span><span class="sxs-lookup"><span data-stu-id="b28cb-180">a.</span></span> <span data-ttu-id="b28cb-181">Guía de administración de "Five9 Plus Adapter for Agent Desktop Toolkit": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="b28cb-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="b28cb-182">b.</span><span class="sxs-lookup"><span data-stu-id="b28cb-182">b.</span></span> <span data-ttu-id="b28cb-183">Guía de administración de "Five9 Plus Adapter for Microsoft Dynamics CRM": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="b28cb-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="b28cb-184">c.</span><span class="sxs-lookup"><span data-stu-id="b28cb-184">c.</span></span> <span data-ttu-id="b28cb-185">Guía de administración de "Five9 Plus Adapter for Zendesk": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="b28cb-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="b28cb-186">Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b28cb-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b28cb-187">Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="b28cb-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b28cb-188">Puede leer más sobre la característica de documentación insertada aquí: [Vista previa: Administración de inicio de sesión único para aplicaciones empresariales en el nuevo Azure Portal]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b28cb-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b28cb-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b28cb-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="b28cb-190">El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b28cb-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b28cb-192">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="b28cb-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b28cb-193">En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b28cb-195">Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b28cb-197">Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b28cb-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b28cb-199">En la página de diálogo **Usuario**, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="b28cb-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b28cb-201">a.</span><span class="sxs-lookup"><span data-stu-id="b28cb-201">a.</span></span> <span data-ttu-id="b28cb-202">En el cuadro de texto **Nombre**, escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b28cb-203">b.</span><span class="sxs-lookup"><span data-stu-id="b28cb-203">b.</span></span> <span data-ttu-id="b28cb-204">En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b28cb-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b28cb-205">c.</span><span class="sxs-lookup"><span data-stu-id="b28cb-205">c.</span></span> <span data-ttu-id="b28cb-206">Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b28cb-207">d.</span><span class="sxs-lookup"><span data-stu-id="b28cb-207">d.</span></span> <span data-ttu-id="b28cb-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="b28cb-209">Creación de un usuario de prueba de Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="b28cb-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="b28cb-210">En esta sección creará un usuario llamado Britta Simon en Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="b28cb-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="b28cb-211">Colabore con el [equipo de soporte técnico de Five9 Plus Adapter (CTI, Contact Center Agents)](https://www.five9.com/about/contact) para agregar los usuarios a la plataforma de Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="b28cb-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add the users in the Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="b28cb-212">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b28cb-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b28cb-213">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b28cb-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b28cb-214">En esta sección habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="b28cb-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Five9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b28cb-216">**Para asignar a Britta Simon a Five9 Plus Adapter (CTI, Contact Center Agents), lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="b28cb-216">**To assign Britta Simon to Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="b28cb-217">En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego, haga clic en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b28cb-219">En la lista de aplicaciones, seleccione **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-219">In the applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. <span data-ttu-id="b28cb-221">En el menú de la izquierda, haga clic en **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b28cb-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-223">Click **Add** button.</span></span> <span data-ttu-id="b28cb-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b28cb-226">En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.</span><span class="sxs-lookup"><span data-stu-id="b28cb-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b28cb-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b28cb-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b28cb-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b28cb-229">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b28cb-229">Testing single sign-on</span></span>

<span data-ttu-id="b28cb-230">En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b28cb-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b28cb-231">Al hacer clic en el icono de Five9 Plus Adapter (CTI, Contact Center Agents) del panel de acceso, debería iniciarse de forma automática la sesión de la aplicación Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="b28cb-231">When you click the Five9 Plus Adapter (CTI, Contact Center Agents) tile in the Access Panel, you should get automatically signed-on to your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="b28cb-232">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b28cb-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b28cb-233">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b28cb-233">Additional resources</span></span>

* [<span data-ttu-id="b28cb-234">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b28cb-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b28cb-235">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b28cb-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

