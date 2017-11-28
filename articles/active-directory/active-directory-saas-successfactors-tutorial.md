---
title: "Tutorial: integración de Azure Active Directory con SuccessFactors | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse SuccessFactors con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="e1886-103">Tutorial: integración de Azure Active Directory con SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="e1886-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="e1886-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate SuccessFactors con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1886-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1886-105">Integración de SuccessFactors con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="e1886-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="e1886-106">Puede controlar en Azure AD que tenga acceso tooSuccessFactors</span><span class="sxs-lookup"><span data-stu-id="e1886-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="e1886-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSuccessFactors (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1886-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="e1886-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e1886-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="e1886-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1886-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1886-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e1886-110">Prerequisites</span></span>
<span data-ttu-id="e1886-111">integración de Azure AD con SuccessFactors tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="e1886-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="e1886-112">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="e1886-112">A valid Azure subscription</span></span>
* <span data-ttu-id="e1886-113">Un inquilino en SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="e1886-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="e1886-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="e1886-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="e1886-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="e1886-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e1886-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e1886-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e1886-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1886-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1886-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="e1886-118">Scenario description</span></span>
<span data-ttu-id="e1886-119">objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="e1886-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="e1886-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="e1886-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1886-121">Agregar SuccessFactors desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e1886-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="e1886-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1886-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="e1886-123">Agregar SuccessFactors desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="e1886-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="e1886-124">integración de hello tooconfigure de SuccessFactors en Azure AD, deberá tooadd SuccessFactors de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="e1886-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1886-125">**tooadd SuccessFactors de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1886-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1886-126">Hola portal de Azure clásico, en el panel de navegación izquierdo hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1886-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Configuración del inicio de sesión único][1]
2. <span data-ttu-id="e1886-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="e1886-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="e1886-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="e1886-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Configuración del inicio de sesión único][2]
4. <span data-ttu-id="e1886-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="e1886-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3]
5. <span data-ttu-id="e1886-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="e1886-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Configuración del inicio de sesión único][4]
6. <span data-ttu-id="e1886-135">Hola **cuadro de búsqueda**, tipo **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="e1886-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Configuración del inicio de sesión único][5]
7. <span data-ttu-id="e1886-137">En el panel de resultados de hello, seleccione **SuccessFactors**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e1886-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Configuración del inicio de sesión único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1886-139">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1886-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1886-140">objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con SuccessFactors a partir de un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e1886-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1886-141">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SuccessFactors tooan usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1886-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="e1886-142">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SuccessFactors debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="e1886-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="e1886-143">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="e1886-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="e1886-144">tooconfigure y prueba de inicio de sesión único en Azure AD con SuccessFactors, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="e1886-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1886-145">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="e1886-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1886-146">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1886-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1886-147">**[Crear un usuario de prueba de SuccessFactors](#creating-a-successfactors-test-user)**  -toohave un equivalente de Britta Simon en SuccessFactors que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="e1886-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="e1886-148">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e1886-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1886-149">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="e1886-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1886-150">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1886-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="e1886-151">En esta sección, habilitar inicio de sesión único en Azure AD en el portal clásico de Hola y configurar el inicio de sesión único en la aplicación de SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="e1886-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="e1886-152">**inicio de sesión único en Azure AD tooconfigure con SuccessFactors, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1886-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1886-153">En el portal de Azure clásico en Hola Hola **SuccessFactors** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1886-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Configuración del inicio de sesión único][7]
2. <span data-ttu-id="e1886-155">En hello **¿cómo desea que los usuarios toosign en tooSuccessFactors** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e1886-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configuración del inicio de sesión único][8]
3. <span data-ttu-id="e1886-157">En hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e1886-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Configuración del inicio de sesión único][9]
   
    <span data-ttu-id="e1886-159">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-159">a.</span></span> <span data-ttu-id="e1886-160">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando uno de hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="e1886-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="e1886-161">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-161">b.</span></span> <span data-ttu-id="e1886-162">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando uno de hello siguiendo patrones:</span><span class="sxs-lookup"><span data-stu-id="e1886-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="e1886-163">c.</span><span class="sxs-lookup"><span data-stu-id="e1886-163">c.</span></span> <span data-ttu-id="e1886-164">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e1886-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e1886-165">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1886-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="e1886-166">Tener tooupdate estos valores con hello URL de dirección URL de inicio de sesión y de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="e1886-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="e1886-167">tooget estos valores, póngase en contacto con [equipo de soporte técnico de SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="e1886-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="e1886-168">En hello **configurar inicio de sesión único en SuccessFactors** página, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e1886-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configuración del inicio de sesión único][10]

2. <span data-ttu-id="e1886-170">En otra ventana del explorador web, inicie sesión en el **Portal de administración de SuccessFactors** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e1886-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="e1886-171">Visite **seguridad de la aplicación** y nativo demasiado**inicio de sesión único en la característica**.</span><span class="sxs-lookup"><span data-stu-id="e1886-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="e1886-172">Colocar cualquier valor en hello **restablecer Token** y haga clic en **guardar Token** tooenable SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="e1886-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación][11]

    > [!NOTE] 
    > <span data-ttu-id="e1886-174">Este valor solo se utiliza como Hola interruptor de encendido/apagado.</span><span class="sxs-lookup"><span data-stu-id="e1886-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="e1886-175">Si se guarda ningún valor, Hola SSO de SAML es ON.</span><span class="sxs-lookup"><span data-stu-id="e1886-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="e1886-176">Si se guarda un valor en blanco Hola SSO de SAML es OFF.</span><span class="sxs-lookup"><span data-stu-id="e1886-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="e1886-177">Captura de pantalla de toobelow nativo y realizar las siguientes acciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1886-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación][12]
   
    <span data-ttu-id="e1886-179">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-179">a.</span></span> <span data-ttu-id="e1886-180">Seleccione hello **SSO de SAML v2** botón de Radio</span><span class="sxs-lookup"><span data-stu-id="e1886-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="e1886-181">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-181">b.</span></span> <span data-ttu-id="e1886-182">Establecer Hola SAML imponer entidad Name(e.g. SAml issuer + company name).</span><span class="sxs-lookup"><span data-stu-id="e1886-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="e1886-183">c.</span><span class="sxs-lookup"><span data-stu-id="e1886-183">c.</span></span> <span data-ttu-id="e1886-184">Hola **emisor SAML** textbox coloca el valor de Hola de **dirección URL del emisor** desde el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1886-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="e1886-185">d.</span><span class="sxs-lookup"><span data-stu-id="e1886-185">d.</span></span> <span data-ttu-id="e1886-186">Seleccione **Response(Customer Generated/IdP/AP)** [Respuesta (cliente generado/IdP/AP)] como **Require Mandatory Signature** (Requerir firma obligatoria).</span><span class="sxs-lookup"><span data-stu-id="e1886-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="e1886-187">e.</span><span class="sxs-lookup"><span data-stu-id="e1886-187">e.</span></span> <span data-ttu-id="e1886-188">Seleccione **Enabled** (Habilitado) como **Enable SAML Flag** (Habilitar marca SAML).</span><span class="sxs-lookup"><span data-stu-id="e1886-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="e1886-189">f.</span><span class="sxs-lookup"><span data-stu-id="e1886-189">f.</span></span> <span data-ttu-id="e1886-190">Seleccione **No** como **Login Request Signature(SF Generated/SP/RP)** [Firma de solicitud de inicio de sesión (SF generado/SP/RP)].</span><span class="sxs-lookup"><span data-stu-id="e1886-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="e1886-191">g.</span><span class="sxs-lookup"><span data-stu-id="e1886-191">g.</span></span> <span data-ttu-id="e1886-192">Seleccione **Browser/Post Profile** (Perfil de explorador/envío) como **SAML Profile** (Perfil SAML).</span><span class="sxs-lookup"><span data-stu-id="e1886-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="e1886-193">h.</span><span class="sxs-lookup"><span data-stu-id="e1886-193">h.</span></span> <span data-ttu-id="e1886-194">Seleccione **No** como **Enforce Certificate Valid Period** (Aplicar período válido de certificado).</span><span class="sxs-lookup"><span data-stu-id="e1886-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="e1886-195">i.</span><span class="sxs-lookup"><span data-stu-id="e1886-195">i.</span></span> <span data-ttu-id="e1886-196">Copiar el contenido de Hola Hola descargado del archivo de certificado y, a continuación, péguelo en hello **el certificado de comprobación SAML** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e1886-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1886-197">contenido del certificado Hola se debe comenzar etiquetas de certificado de certificado y de cierre.</span><span class="sxs-lookup"><span data-stu-id="e1886-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="e1886-198">Navegue tooSAML V2 y, a continuación, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e1886-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Configuración del inicio de sesión único en la aplicación][13]
   
    <span data-ttu-id="e1886-200">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-200">a.</span></span> <span data-ttu-id="e1886-201">Seleccione **Yes** (Sí) como **Support SP-initiated Global Logout** (Permitir cierre de sesión global iniciado por SP).</span><span class="sxs-lookup"><span data-stu-id="e1886-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="e1886-202">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-202">b.</span></span> <span data-ttu-id="e1886-203">Hola **URL del servicio de cierre de sesión Global (destino de LogoutRequest)** textbox coloca el valor de Hola de **dirección URL de cierre de sesión remoto** desde el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1886-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="e1886-204">c.</span><span class="sxs-lookup"><span data-stu-id="e1886-204">c.</span></span> <span data-ttu-id="e1886-205">Seleccione **No** en **Require sp must encrypt all NameID element** (Requerir que sp cifre todos los elementos NameID).</span><span class="sxs-lookup"><span data-stu-id="e1886-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="e1886-206">d.</span><span class="sxs-lookup"><span data-stu-id="e1886-206">d.</span></span> <span data-ttu-id="e1886-207">Seleccione **Unspecified** (Sin especificar) como **NameID Format** (Formato de NameID).</span><span class="sxs-lookup"><span data-stu-id="e1886-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="e1886-208">e.</span><span class="sxs-lookup"><span data-stu-id="e1886-208">e.</span></span> <span data-ttu-id="e1886-209">Seleccione **Yes** (Sí) como **Enable sp initiated login (AuthnRequest)** [Permitir inicio de sesión iniciado por sp (AuthnRequest)].</span><span class="sxs-lookup"><span data-stu-id="e1886-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="e1886-210">f.</span><span class="sxs-lookup"><span data-stu-id="e1886-210">f.</span></span> <span data-ttu-id="e1886-211">Hola **solicitud de envío como emisor de toda la empresa** textbox coloca el valor de Hola de **dirección URL de inicio de sesión remoto** desde el Asistente para configuración de aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1886-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="e1886-212">Siga estos pasos si desea que los nombres de usuario de inicio de sesión de toomake Hola distingue entre mayúsculas y minúsculas,.</span><span class="sxs-lookup"><span data-stu-id="e1886-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="e1886-213">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-213">a.</span></span> <span data-ttu-id="e1886-214">Visite **configuración de la empresa**(cerca de la parte inferior de hello).</span><span class="sxs-lookup"><span data-stu-id="e1886-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="e1886-215">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-215">b.</span></span> <span data-ttu-id="e1886-216">Seleccione la casilla junto a **Enable Non-Case-Sensitive Username**(Habilitar nombre de usuario sin distinción de mayúsculas y minúsculas).</span><span class="sxs-lookup"><span data-stu-id="e1886-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="e1886-217">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="e1886-217">c.Click **Save**.</span></span>
   
    ![Configurar inicio de sesión único][29]

    > [!NOTE] 
    > <span data-ttu-id="e1886-219">Si intentas tooenable esto, sistema de hello comprueba si se creará un nombre de inicio de sesión SAML duplicado.</span><span class="sxs-lookup"><span data-stu-id="e1886-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="e1886-220">Por ejemplo, si el cliente de hello tiene nombres de usuario User1 y user1.</span><span class="sxs-lookup"><span data-stu-id="e1886-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="e1886-221">Al no distinguir mayúsculas de minúsculas, estos nombres pasan a ser duplicados.</span><span class="sxs-lookup"><span data-stu-id="e1886-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="e1886-222">sistema de Hello le proporcionará un mensaje de error y no habilitará la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e1886-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="e1886-223">Hola cliente deberá toochange uno de los nombres de usuario de Hola por lo que se ha escrito realmente diferentes.</span><span class="sxs-lookup"><span data-stu-id="e1886-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="e1886-224">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e1886-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Aplicaciones][14]
2. <span data-ttu-id="e1886-226">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="e1886-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Aplicaciones][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1886-228">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1886-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1886-229">objetivo de Hola de esta sección es toocreate un usuario de prueba en el portal clásico de hello llamado a Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1886-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][16]

<span data-ttu-id="e1886-231">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1886-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1886-232">Hola **Portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e1886-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][17]
2. <span data-ttu-id="e1886-234">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="e1886-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="e1886-235">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e1886-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][18]
4. <span data-ttu-id="e1886-237">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="e1886-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][19]
5. <span data-ttu-id="e1886-239">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e1886-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][20]
   
    <span data-ttu-id="e1886-241">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-241">a.</span></span> <span data-ttu-id="e1886-242">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="e1886-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="e1886-243">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-243">b.</span></span> <span data-ttu-id="e1886-244">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1886-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="e1886-245">c.</span><span class="sxs-lookup"><span data-stu-id="e1886-245">c.</span></span> <span data-ttu-id="e1886-246">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e1886-246">Click **Next**.</span></span>
6. <span data-ttu-id="e1886-247">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e1886-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][21]
   
    <span data-ttu-id="e1886-249">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-249">a.</span></span> <span data-ttu-id="e1886-250">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="e1886-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="e1886-251">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-251">b.</span></span> <span data-ttu-id="e1886-252">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e1886-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="e1886-253">c.</span><span class="sxs-lookup"><span data-stu-id="e1886-253">c.</span></span> <span data-ttu-id="e1886-254">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e1886-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="e1886-255">d.</span><span class="sxs-lookup"><span data-stu-id="e1886-255">d.</span></span> <span data-ttu-id="e1886-256">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="e1886-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="e1886-257">e.</span><span class="sxs-lookup"><span data-stu-id="e1886-257">e.</span></span> <span data-ttu-id="e1886-258">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="e1886-258">Click **Next**.</span></span>
7. <span data-ttu-id="e1886-259">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="e1886-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][22]
8. <span data-ttu-id="e1886-261">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="e1886-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][23]
   
    <span data-ttu-id="e1886-263">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-263">a.</span></span> <span data-ttu-id="e1886-264">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e1886-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="e1886-265">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-265">b.</span></span> <span data-ttu-id="e1886-266">Haga clic en **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e1886-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="e1886-267">Creación de un usuario de prueba de SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="e1886-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="e1886-268">En orden tooenable toolog de los usuarios de Azure AD en SuccessFactors, se les deben aprovisionar en SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="e1886-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="e1886-269">En caso de hello de SuccessFactors, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="e1886-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="e1886-270">tooget los usuarios creados en SuccessFactors, necesita hello toocontact [equipo de soporte técnico de SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="e1886-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e1886-271">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1886-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="e1886-272">objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooSuccessFactors de acceso.</span><span class="sxs-lookup"><span data-stu-id="e1886-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Asignar usuario][24]

<span data-ttu-id="e1886-274">**tooassign Britta Simon tooSuccessFactors, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="e1886-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1886-275">En el portal clásico de hello, haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="e1886-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Asignar usuario][25]
2. <span data-ttu-id="e1886-277">En la lista de aplicaciones de hello, seleccione **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="e1886-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Configurar inicio de sesión único][26]
3. <span data-ttu-id="e1886-279">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="e1886-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Asignar usuario][27]
4. <span data-ttu-id="e1886-281">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e1886-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e1886-282">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="e1886-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="e1886-284">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="e1886-284">Testing single sign-on</span></span>
<span data-ttu-id="e1886-285">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e1886-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1886-286">Al hacer clic en hello SuccessFactors disponer en mosaico en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour aplicación de SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="e1886-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1886-287">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="e1886-287">Additional resources</span></span>
* [<span data-ttu-id="e1886-288">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1886-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1886-289">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e1886-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
