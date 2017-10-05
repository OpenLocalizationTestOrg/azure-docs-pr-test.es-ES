---
title: "Tutorial: Integración de Azure Active Directory con Questetra BPM Suite | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="56244-103">Tutorial: Integración de Azure Active Directory con Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="56244-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="56244-104">El objetivo de este tutorial es mostrar cómo integrar Questetra BPM Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56244-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="56244-105">La integración de Questetra BPM Suite con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="56244-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="56244-106">Puede controlar en Azure AD quién tiene acceso a Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="56244-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="56244-107">Puede permitir que los usuarios inicien sesión automáticamente en Questetra BPM Suite (inicio de sesión único) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56244-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="56244-108">Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="56244-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="56244-109">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56244-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56244-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="56244-110">Prerequisites</span></span>
<span data-ttu-id="56244-111">Para configurar la integración de Azure AD con Questetra BPM Suite, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="56244-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="56244-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56244-112">An Azure AD subscription</span></span>
* <span data-ttu-id="56244-113">Una suscripción habilitada para el inicio de sesión único en [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/)</span><span class="sxs-lookup"><span data-stu-id="56244-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56244-114">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="56244-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="56244-115">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="56244-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="56244-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="56244-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="56244-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56244-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="56244-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="56244-118">Scenario Description</span></span>
<span data-ttu-id="56244-119">El objetivo de este tutorial es permitirle probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="56244-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="56244-120">El escenario descrito en este tutorial consta de tres bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="56244-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="56244-121">Incorporación de Questetra BPM Suite desde la galería</span><span class="sxs-lookup"><span data-stu-id="56244-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="56244-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56244-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="56244-123">Incorporación de Questetra BPM Suite desde la galería</span><span class="sxs-lookup"><span data-stu-id="56244-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="56244-124">Para configurar la integración de Questetra BPM Suite en Azure AD, deberá agregar Questetra BPM Suite desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="56244-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56244-125">**Para agregar Questetra BPM Suite desde la galería, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="56244-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56244-126">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56244-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="56244-128">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="56244-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="56244-129">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="56244-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="56244-131">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="56244-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicaciones][3]

5. <span data-ttu-id="56244-133">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="56244-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicaciones][4]

6. <span data-ttu-id="56244-135">En el cuadro de búsqueda, escriba **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="56244-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Aplicaciones][5]

7. <span data-ttu-id="56244-137">En el panel de resultados, seleccione **Questetra BPM Suite** y, después, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="56244-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56244-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56244-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56244-139">El objetivo de esta sección es mostrar cómo configurar y probar el inicio de sesión único de Azure AD con Questetra BPM Suite con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56244-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56244-140">Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Questetra BPM Suite para un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56244-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="56244-141">Es decir, se requiere establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="56244-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="56244-142">Para establecer esta relación de vínculo, se asigna el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="56244-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="56244-143">Para configurar y probar el inicio de sesión único de Azure AD con Questetra BPM Suite, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="56244-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56244-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on)** : para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="56244-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56244-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56244-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56244-146">**[Creación de un usuario de prueba de Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)** : para tener un homólogo de Britta Simon en Questetra BPM Suite que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56244-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="56244-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56244-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56244-148">**[Prueba del inicio de sesión único](#testing-single-sign-on)** : para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="56244-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56244-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56244-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="56244-150">El objetivo de esta sección es habilitar el inicio de sesión único de Azure AD en el Portal de Azure clásico y configurar el inicio de sesión único en la aplicación Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="56244-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="56244-151">**Para configurar el inicio de sesión único de Azure AD con Questetra BPM Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="56244-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="56244-152">En el Portal de Azure clásico, en la página de integración de aplicaciones de **Questetra BPM Suite**, haga clic en **Configurar inicio de sesión único** para abrir el diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="56244-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][8]

2. <span data-ttu-id="56244-154">En la página **¿Cómo desea que los usuarios inicien sesión en Questetra BPM Suite?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56244-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][9]

3. <span data-ttu-id="56244-156">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de **Questetra BPM Suite** como administrador.</span><span class="sxs-lookup"><span data-stu-id="56244-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="56244-157">En el menú de la parte superior, haga clic en **Configuración del sistema**.</span><span class="sxs-lookup"><span data-stu-id="56244-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][10]

5. <span data-ttu-id="56244-159">Para abrir la página **SingleSignOnSAML**, haga clic en **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="56244-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][11]

6. <span data-ttu-id="56244-161">En el Portal de Azure clásico, en la página de diálogo **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56244-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configurar las opciones de la aplicación][13]
   
    <span data-ttu-id="56244-163">a.</span><span class="sxs-lookup"><span data-stu-id="56244-163">a.</span></span> <span data-ttu-id="56244-164">En el sitio de la compañía de **Questetra BPM Suite**, en la sección de información de SP, copie la **URL de ACS** y, después, péguela en el cuadro de texto **URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="56244-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="56244-165">b.</span><span class="sxs-lookup"><span data-stu-id="56244-165">b.</span></span> <span data-ttu-id="56244-166">En el sitio de la compañía de **Questetra BPM Suite**, en la sección de información de SP, copie el valor de **Entity ID** (Id. de entidad) y, después, péguelo en el cuadro de texto **URL del emisor**.</span><span class="sxs-lookup"><span data-stu-id="56244-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="56244-167">c.</span><span class="sxs-lookup"><span data-stu-id="56244-167">c.</span></span> <span data-ttu-id="56244-168">En el sitio de la compañía de **Questetra BPM Suite**, en la sección de información de SP, copie el valor de **URL de ACS** y, después, péguelo en el cuadro de texto **URL de respuesta**.</span><span class="sxs-lookup"><span data-stu-id="56244-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="56244-169">d.</span><span class="sxs-lookup"><span data-stu-id="56244-169">d.</span></span> <span data-ttu-id="56244-170">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56244-170">Click **Next**.</span></span>

7. <span data-ttu-id="56244-171">En la página **Configurar inicio de sesión único en Questetra BPM Suite**, haga clic en **Descargar certificado** y guarde el archivo de certificado de forma local en el equipo.</span><span class="sxs-lookup"><span data-stu-id="56244-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configurar inicio de sesión único][14]

8. <span data-ttu-id="56244-173">En el sitio de la compañía **Questetra BPM Suite** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56244-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Configurar inicio de sesión único][15]
   
    <span data-ttu-id="56244-175">a.</span><span class="sxs-lookup"><span data-stu-id="56244-175">a.</span></span> <span data-ttu-id="56244-176">Seleccione **Enable Single Sign-On**(Habilitar inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="56244-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="56244-177">b.</span><span class="sxs-lookup"><span data-stu-id="56244-177">b.</span></span> <span data-ttu-id="56244-178">En el Portal de Azure clásico, copie el valor de **URL del emisor** y péguelo en el cuadro de texto **Id. de entidad**.</span><span class="sxs-lookup"><span data-stu-id="56244-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="56244-179">c.</span><span class="sxs-lookup"><span data-stu-id="56244-179">c.</span></span> <span data-ttu-id="56244-180">En el Portal de Azure clásico, copie el valor de **Dirección URL del servicio de inicio de sesión único** y péguelo en el cuadro de texto **Dirección URL de la página de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="56244-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="56244-181">d.</span><span class="sxs-lookup"><span data-stu-id="56244-181">d.</span></span> <span data-ttu-id="56244-182">En el Portal de Azure clásico, copie el valor de **Dirección URL del servicio de cierre de sesión único** y péguelo en el cuadro de texto **Dirección URL de la página de cierre de sesión**.</span><span class="sxs-lookup"><span data-stu-id="56244-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="56244-183">e.</span><span class="sxs-lookup"><span data-stu-id="56244-183">e.</span></span> <span data-ttu-id="56244-184">En el cuadro de texto **NameID format** (Formato de id. de nombre), escriba **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="56244-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="56244-185">f.</span><span class="sxs-lookup"><span data-stu-id="56244-185">f.</span></span> <span data-ttu-id="56244-186">Cree un archivo codificado en base 64 a partir del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="56244-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="56244-187">Para obtener más información, consulte [Conversión de un certificado binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="56244-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="56244-188">g.</span><span class="sxs-lookup"><span data-stu-id="56244-188">g.</span></span> <span data-ttu-id="56244-189">Abra el certificado codificado en base 64 en el Bloc de notas, copie su contenido en el Portapapeles y, a continuación, péguelo en el cuadro de texto **Certificado de validación** .</span><span class="sxs-lookup"><span data-stu-id="56244-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="56244-190">h.</span><span class="sxs-lookup"><span data-stu-id="56244-190">h.</span></span> <span data-ttu-id="56244-191">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="56244-191">Click **Save**.</span></span>

1. <span data-ttu-id="56244-192">En el Portal de Azure clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56244-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Qué es Azure AD Connect][17]

2. <span data-ttu-id="56244-194">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="56244-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Qué es Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56244-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56244-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="56244-197">El objetivo de esta sección es crear un usuario de prueba en el Portal de Azure clásico llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56244-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="56244-198">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="56244-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56244-199">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56244-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][100] 

2. <span data-ttu-id="56244-201">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="56244-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="56244-202">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="56244-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][101] 

4. <span data-ttu-id="56244-204">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="56244-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD][102] 

5. <span data-ttu-id="56244-206">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56244-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][103]
   
    <span data-ttu-id="56244-208">a.</span><span class="sxs-lookup"><span data-stu-id="56244-208">a.</span></span> <span data-ttu-id="56244-209">En **Tipo de usuario**, seleccione **Nuevo usuario de la organización**.</span><span class="sxs-lookup"><span data-stu-id="56244-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="56244-210">b.</span><span class="sxs-lookup"><span data-stu-id="56244-210">b.</span></span> <span data-ttu-id="56244-211">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56244-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="56244-212">c.</span><span class="sxs-lookup"><span data-stu-id="56244-212">c.</span></span> <span data-ttu-id="56244-213">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="56244-213">Click Next.</span></span>

6. <span data-ttu-id="56244-214">En la página de diálogo **Perfil de usuario** , realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="56244-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD][104] 
   
    <span data-ttu-id="56244-216">a.</span><span class="sxs-lookup"><span data-stu-id="56244-216">a.</span></span> <span data-ttu-id="56244-217">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="56244-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="56244-218">b.</span><span class="sxs-lookup"><span data-stu-id="56244-218">b.</span></span> <span data-ttu-id="56244-219">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="56244-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="56244-220">c.</span><span class="sxs-lookup"><span data-stu-id="56244-220">c.</span></span> <span data-ttu-id="56244-221">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="56244-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="56244-222">d.</span><span class="sxs-lookup"><span data-stu-id="56244-222">d.</span></span> <span data-ttu-id="56244-223">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="56244-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="56244-224">e.</span><span class="sxs-lookup"><span data-stu-id="56244-224">e.</span></span> <span data-ttu-id="56244-225">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="56244-225">Click **Next**.</span></span>

7. <span data-ttu-id="56244-226">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="56244-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][105]  

8. <span data-ttu-id="56244-228">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56244-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][106]   
   
    <span data-ttu-id="56244-230">a.</span><span class="sxs-lookup"><span data-stu-id="56244-230">a.</span></span> <span data-ttu-id="56244-231">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="56244-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="56244-232">b.</span><span class="sxs-lookup"><span data-stu-id="56244-232">b.</span></span> <span data-ttu-id="56244-233">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="56244-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="56244-234">Creación de un usuario de prueba de Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="56244-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="56244-235">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="56244-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="56244-236">**Para crear un usuario llamado Britta Simon en Questetra BPM Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="56244-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="56244-237">Inicie sesión en el sitio de la compañía de Questetra BPM Suite como administrador.</span><span class="sxs-lookup"><span data-stu-id="56244-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="56244-238">Vaya a **System Settings > User List > New User** (Configuración del sistema > Lista de usuarios > Nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="56244-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="56244-239">En el cuadro de diálogo Nuevo usuario, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56244-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Creación de un usuario de prueba][300] 
   
    <span data-ttu-id="56244-241">a.</span><span class="sxs-lookup"><span data-stu-id="56244-241">a.</span></span> <span data-ttu-id="56244-242">En el cuadro de texto **Name** (Nombre), escriba el nombre de usuario de Britta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56244-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="56244-243">b.</span><span class="sxs-lookup"><span data-stu-id="56244-243">b.</span></span> <span data-ttu-id="56244-244">En el cuadro de texto **Email** (Correo electrónico), escriba el nombre de usuario de Britta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56244-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="56244-245">c.</span><span class="sxs-lookup"><span data-stu-id="56244-245">c.</span></span> <span data-ttu-id="56244-246">En el cuadro de texto **Password** (Contraseña), escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="56244-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="56244-247">Haga clic en **Add new user**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="56244-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56244-248">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="56244-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="56244-249">El objetivo de esta sección es permitir que Britta Simon use el inicio de sesión único de Azure al concederle acceso a Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="56244-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![Qué es Azure AD Connect][200]

<span data-ttu-id="56244-251">**Para asignar Britta Simon a Questetra BPM Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="56244-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="56244-252">En el Portal de Azure clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en la opción **Aplicaciones** del menú superior.</span><span class="sxs-lookup"><span data-stu-id="56244-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Qué es Azure AD Connect][201]
2. <span data-ttu-id="56244-254">En la lista de aplicaciones, seleccione **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="56244-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Qué es Azure AD Connect][205]
3. <span data-ttu-id="56244-256">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="56244-256">In the menu on the top, click **Users**.</span></span>
   
    ![Qué es Azure AD Connect][202]
4. <span data-ttu-id="56244-258">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="56244-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![Qué es Azure AD Connect][203]
5. <span data-ttu-id="56244-260">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="56244-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Qué es Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="56244-262">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="56244-262">Testing Single Sign-On</span></span>
<span data-ttu-id="56244-263">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="56244-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="56244-264">Al hacer clic en el icono Questetra BPM Suite en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación de Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="56244-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56244-265">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="56244-265">Additional Resources</span></span>
* [<span data-ttu-id="56244-266">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56244-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56244-267">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56244-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
