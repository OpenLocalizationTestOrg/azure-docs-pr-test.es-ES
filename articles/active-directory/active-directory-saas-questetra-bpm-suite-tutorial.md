---
title: "Tutorial: Integración de Azure Active Directory con Questetra BPM Suite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Questetra BPM Suite."
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
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="3461b-103">Tutorial: Integración de Azure Active Directory con Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="3461b-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="3461b-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate Questetra BPM Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3461b-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="3461b-105">Integración Questetra BPM Suite con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3461b-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="3461b-106">Puede controlar en Azure AD que tenga acceso tooQuestetra conjunto de BPM</span><span class="sxs-lookup"><span data-stu-id="3461b-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="3461b-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooQuestetra BPM Suite (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3461b-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="3461b-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="3461b-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="3461b-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3461b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3461b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3461b-110">Prerequisites</span></span>
<span data-ttu-id="3461b-111">integración de Azure AD con Questetra BPM Suite tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3461b-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="3461b-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3461b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="3461b-113">Una suscripción habilitada para el inicio de sesión único en [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/)</span><span class="sxs-lookup"><span data-stu-id="3461b-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3461b-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3461b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="3461b-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3461b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="3461b-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3461b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="3461b-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3461b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="3461b-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3461b-118">Scenario Description</span></span>
<span data-ttu-id="3461b-119">objetivo de Hola de este tutorial es tooenable tootest inicio de sesión único en Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3461b-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="3461b-120">escenario de Hello descrito en este tutorial consta de tres pilares principales:</span><span class="sxs-lookup"><span data-stu-id="3461b-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="3461b-121">Agregar conjunto de BPM Questetra desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="3461b-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="3461b-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3461b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="3461b-123">Agregar conjunto de BPM Questetra desde galería Hola</span><span class="sxs-lookup"><span data-stu-id="3461b-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="3461b-124">integración de hello tooconfigure de Questetra BPM Suite en Azure AD, deberá tooadd Questetra BPM Suite de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3461b-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3461b-125">**tooadd Questetra BPM Suite de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3461b-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3461b-126">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3461b-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="3461b-128">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="3461b-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3461b-129">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="3461b-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicaciones][2]

4. <span data-ttu-id="3461b-131">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="3461b-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3]

5. <span data-ttu-id="3461b-133">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="3461b-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicaciones][4]

6. <span data-ttu-id="3461b-135">En el cuadro de búsqueda de hello, escriba **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="3461b-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Aplicaciones][5]

7. <span data-ttu-id="3461b-137">En el panel de resultados de hello, seleccione **Questetra BPM Suite**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="3461b-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3461b-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3461b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3461b-139">objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de inicio de sesión único en Azure AD con Questetra BPM Suite a partir de un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3461b-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3461b-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow es qué usuario equivalente de hello en usuario de tooan Questetra BPM Suite en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3461b-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="3461b-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en el conjunto de BPM Questetra debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3461b-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="3461b-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="3461b-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="3461b-143">tooconfigure y prueba de inicio de sesión único en Azure AD con Questetra BPM Suite, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3461b-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3461b-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3461b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3461b-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3461b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3461b-146">**[Crear un usuario de prueba del conjunto de BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  -toohave un equivalente de Britta Simon Questetra BPM conjunto de representación toohello vinculado Azure AD de ella.</span><span class="sxs-lookup"><span data-stu-id="3461b-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="3461b-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3461b-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3461b-148">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3461b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3461b-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3461b-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="3461b-150">objetivo de Hola de esta sección es tooenable Azure AD single sign-on en hello portal de Azure clásico y tooconfigure inicio de sesión único en la aplicación Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="3461b-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="3461b-151">**tooconfigure inicio de sesión único en Azure AD con Questetra BPM Suite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3461b-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3461b-152">En el portal de Azure clásico en Hola Hola **Questetra BPM Suite** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3461b-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][8]

2. <span data-ttu-id="3461b-154">En hello **¿cómo desea que los usuarios toosign en tooQuestetra BPM Suite** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3461b-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][9]

3. <span data-ttu-id="3461b-156">En otra ventana del explorador web, inicie sesión en el sitio de la compañía de **Questetra BPM Suite** como administrador.</span><span class="sxs-lookup"><span data-stu-id="3461b-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="3461b-157">En el menú de hello en la parte superior de hello, haga clic en **configuración del sistema**.</span><span class="sxs-lookup"><span data-stu-id="3461b-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][10]

5. <span data-ttu-id="3461b-159">Hola tooopen **SingleSignOnSAML** página, haga clic en **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="3461b-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][11]

6. <span data-ttu-id="3461b-161">En el portal de Azure clásico en Hola Hola **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3461b-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Configurar las opciones de la aplicación][13]
   
    <span data-ttu-id="3461b-163">a.</span><span class="sxs-lookup"><span data-stu-id="3461b-163">a.</span></span> <span data-ttu-id="3461b-164">Depende de usted **Questetra BPM Suite** sitio de la empresa, en la sección de información de SP hello, Hola copia **dirección URL de ACS**y, a continuación, péguelo en hello **dirección URL de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3461b-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="3461b-165">b.</span><span class="sxs-lookup"><span data-stu-id="3461b-165">b.</span></span> <span data-ttu-id="3461b-166">Depende de usted **Questetra BPM Suite** sitio de la empresa, en la sección de información de SP hello, Hola copia **Id. de entidad**y, a continuación, péguelo en hello **dirección URL del emisor** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3461b-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="3461b-167">c.</span><span class="sxs-lookup"><span data-stu-id="3461b-167">c.</span></span> <span data-ttu-id="3461b-168">Depende de usted **Questetra BPM Suite** sitio de la empresa, en la sección de información de SP hello, Hola copia **dirección URL de ACS**y, a continuación, péguelo en hello **dirección URL de respuesta** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3461b-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="3461b-169">d.</span><span class="sxs-lookup"><span data-stu-id="3461b-169">d.</span></span> <span data-ttu-id="3461b-170">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3461b-170">Click **Next**.</span></span>

7. <span data-ttu-id="3461b-171">En hello **configurar inicio de sesión único en el conjunto de BPM Questetra** página, haga clic en **Descargar certificado**y, a continuación, guarde el archivo de certificado de hello localmente en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3461b-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configurar inicio de sesión único][14]

8. <span data-ttu-id="3461b-173">Depende de usted **Questetra BPM Suite** sitio de la compañía, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3461b-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Configurar inicio de sesión único][15]
   
    <span data-ttu-id="3461b-175">a.</span><span class="sxs-lookup"><span data-stu-id="3461b-175">a.</span></span> <span data-ttu-id="3461b-176">Seleccione **Enable Single Sign-On**(Habilitar inicio de sesión único).</span><span class="sxs-lookup"><span data-stu-id="3461b-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="3461b-177">b.</span><span class="sxs-lookup"><span data-stu-id="3461b-177">b.</span></span> <span data-ttu-id="3461b-178">En el portal de Azure clásico hello, copie hello **dirección URL del emisor** valor y, a continuación, péguelo en hello **Id. de entidad** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3461b-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="3461b-179">c.</span><span class="sxs-lookup"><span data-stu-id="3461b-179">c.</span></span> <span data-ttu-id="3461b-180">En el portal de Azure clásico hello, copie hello **URL de servicio de inicio de sesión único** valor y, a continuación, péguelo en hello **URL de la página de inicio de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3461b-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="3461b-181">d.</span><span class="sxs-lookup"><span data-stu-id="3461b-181">d.</span></span> <span data-ttu-id="3461b-182">En el portal de Azure clásico hello, copie hello **dirección URL del servicio de cierre de sesión único** valor y, a continuación, péguelo en hello **URL de la página de cierre de sesión** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3461b-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="3461b-183">e.</span><span class="sxs-lookup"><span data-stu-id="3461b-183">e.</span></span> <span data-ttu-id="3461b-184">Hola **formato de NameID** cuadro de texto, tipo **urn: oasis: nombres: tc: SAML:1.1:nameid-formato: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="3461b-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="3461b-185">f.</span><span class="sxs-lookup"><span data-stu-id="3461b-185">f.</span></span> <span data-ttu-id="3461b-186">Cree un archivo codificado en base 64 a partir del certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="3461b-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="3461b-187">Para obtener más información, consulte [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="3461b-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="3461b-188">g.</span><span class="sxs-lookup"><span data-stu-id="3461b-188">g.</span></span> <span data-ttu-id="3461b-189">Abra el certificado codificado en base 64 en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo en hello **certificado de validación** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="3461b-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="3461b-190">h.</span><span class="sxs-lookup"><span data-stu-id="3461b-190">h.</span></span> <span data-ttu-id="3461b-191">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3461b-191">Click **Save**.</span></span>

1. <span data-ttu-id="3461b-192">En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3461b-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Qué es Azure AD Connect][17]

2. <span data-ttu-id="3461b-194">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="3461b-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Qué es Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3461b-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3461b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="3461b-197">objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="3461b-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="3461b-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3461b-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3461b-199">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3461b-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][100] 

2. <span data-ttu-id="3461b-201">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="3461b-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="3461b-202">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3461b-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][101] 

4. <span data-ttu-id="3461b-204">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="3461b-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD][102] 

5. <span data-ttu-id="3461b-206">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3461b-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][103]
   
    <span data-ttu-id="3461b-208">a.</span><span class="sxs-lookup"><span data-stu-id="3461b-208">a.</span></span> <span data-ttu-id="3461b-209">En **Tipo de usuario**, seleccione **Nuevo usuario de la organización**.</span><span class="sxs-lookup"><span data-stu-id="3461b-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="3461b-210">b.</span><span class="sxs-lookup"><span data-stu-id="3461b-210">b.</span></span> <span data-ttu-id="3461b-211">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3461b-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="3461b-212">c.</span><span class="sxs-lookup"><span data-stu-id="3461b-212">c.</span></span> <span data-ttu-id="3461b-213">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="3461b-213">Click Next.</span></span>

6. <span data-ttu-id="3461b-214">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3461b-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD][104] 
   
    <span data-ttu-id="3461b-216">a.</span><span class="sxs-lookup"><span data-stu-id="3461b-216">a.</span></span> <span data-ttu-id="3461b-217">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="3461b-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="3461b-218">b.</span><span class="sxs-lookup"><span data-stu-id="3461b-218">b.</span></span> <span data-ttu-id="3461b-219">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3461b-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="3461b-220">c.</span><span class="sxs-lookup"><span data-stu-id="3461b-220">c.</span></span> <span data-ttu-id="3461b-221">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3461b-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="3461b-222">d.</span><span class="sxs-lookup"><span data-stu-id="3461b-222">d.</span></span> <span data-ttu-id="3461b-223">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="3461b-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="3461b-224">e.</span><span class="sxs-lookup"><span data-stu-id="3461b-224">e.</span></span> <span data-ttu-id="3461b-225">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3461b-225">Click **Next**.</span></span>

7. <span data-ttu-id="3461b-226">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="3461b-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][105]  

8. <span data-ttu-id="3461b-228">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3461b-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD][106]   
   
    <span data-ttu-id="3461b-230">a.</span><span class="sxs-lookup"><span data-stu-id="3461b-230">a.</span></span> <span data-ttu-id="3461b-231">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3461b-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="3461b-232">b.</span><span class="sxs-lookup"><span data-stu-id="3461b-232">b.</span></span> <span data-ttu-id="3461b-233">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="3461b-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="3461b-234">Creación de un usuario de prueba de Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="3461b-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="3461b-235">objetivo de Hola de esta sección es toocreate un usuario llamado a Britta Simon en Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="3461b-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="3461b-236">**toocreate un usuario llamado Britta Simon en Questetra BPM Suite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3461b-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3461b-237">Sitio de empresa de Questetra BPM Suite tooyour inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="3461b-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="3461b-238">Vaya demasiado**configuración del sistema > lista de usuarios > nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="3461b-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="3461b-239">Cuadro de diálogo nuevo usuario de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3461b-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Creación de un usuario de prueba][300] 
   
    <span data-ttu-id="3461b-241">a.</span><span class="sxs-lookup"><span data-stu-id="3461b-241">a.</span></span> <span data-ttu-id="3461b-242">Hola **nombre** cuadro de texto, escriba el nombre de usuario de Bárbara en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3461b-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="3461b-243">b.</span><span class="sxs-lookup"><span data-stu-id="3461b-243">b.</span></span> <span data-ttu-id="3461b-244">Hola **correo electrónico** cuadro de texto, escriba el nombre de usuario de Bárbara en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3461b-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="3461b-245">c.</span><span class="sxs-lookup"><span data-stu-id="3461b-245">c.</span></span> <span data-ttu-id="3461b-246">Hola **contraseña** cuadro de texto, escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="3461b-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="3461b-247">Haga clic en **Add new user**(Agregar nuevo usuario).</span><span class="sxs-lookup"><span data-stu-id="3461b-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3461b-248">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3461b-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="3461b-249">objetivo de Hola de esta sección es tooenabling Britta Simon toouse Azure inicio de sesión único mediante la concesión de su conjunto de BPM tooQuestetra de acceso.</span><span class="sxs-lookup"><span data-stu-id="3461b-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Qué es Azure AD Connect][200]

<span data-ttu-id="3461b-251">**tooassign Britta Simon tooQuestetra BPM Suite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3461b-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="3461b-252">En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="3461b-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Qué es Azure AD Connect][201]
2. <span data-ttu-id="3461b-254">En la lista de aplicaciones de hello, seleccione **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="3461b-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Qué es Azure AD Connect][205]
3. <span data-ttu-id="3461b-256">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3461b-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Qué es Azure AD Connect][202]
4. <span data-ttu-id="3461b-258">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3461b-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Qué es Azure AD Connect][203]
5. <span data-ttu-id="3461b-260">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="3461b-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Qué es Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="3461b-262">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3461b-262">Testing Single Sign-On</span></span>
<span data-ttu-id="3461b-263">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3461b-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="3461b-264">Al hacer clic en icono de conjunto de BPM Questetra Hola Hola Panel de acceso, deberá obtener la aplicación de conjunto de BPM Questetra tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="3461b-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3461b-265">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3461b-265">Additional Resources</span></span>
* [<span data-ttu-id="3461b-266">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3461b-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3461b-267">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3461b-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
