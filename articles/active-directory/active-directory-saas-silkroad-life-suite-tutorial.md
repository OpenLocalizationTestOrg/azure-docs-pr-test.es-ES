---
title: "Tutorial: Integración de Azure Active Directory con SilkRoad Life Suite | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SilkRoad vida Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="49ddd-103">Tutorial: Integración de Azure Active Directory con SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="49ddd-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="49ddd-104">objetivo de Hola de este tutorial es tooshow, cómo toointegrate SilkRoad vida Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49ddd-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="49ddd-105">Integración SilkRoad vida Suite con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="49ddd-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="49ddd-106">Puede controlar en Azure AD que tenga acceso tooSilkRoad Suite de vida</span><span class="sxs-lookup"><span data-stu-id="49ddd-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="49ddd-107">Puede habilitar la get ha iniciado sesión tooSilkRoad de usuarios tooautomatically vida Suite inicio de sesión único (SSO) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ddd-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="49ddd-108">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49ddd-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49ddd-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="49ddd-109">Prerequisites</span></span>
<span data-ttu-id="49ddd-110">integración de Azure AD con Suite de vida de SilkRoad tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="49ddd-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="49ddd-111">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ddd-111">An Azure AD subscription</span></span>
* <span data-ttu-id="49ddd-112">Una suscripción habilitada para el SSO en SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="49ddd-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="49ddd-113">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="49ddd-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="49ddd-114">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="49ddd-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="49ddd-115">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="49ddd-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="49ddd-116">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49ddd-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="49ddd-117">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="49ddd-117">Scenario Description</span></span>
<span data-ttu-id="49ddd-118">objetivo de Hola de este tutorial es tooenable tootest Azure AD SSO en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="49ddd-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="49ddd-119">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="49ddd-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49ddd-120">Agregar conjunto de vida de SilkRoad de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="49ddd-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="49ddd-121">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ddd-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="49ddd-122">Agregar conjunto de vida de SilkRoad de galería de Hola</span><span class="sxs-lookup"><span data-stu-id="49ddd-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="49ddd-123">integración de hello tooconfigure del conjunto de vida SilkRoad en Azure AD, deberá tooadd SilkRoad vida Suite de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="49ddd-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49ddd-124">**tooadd SilkRoad Suite de vida de la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="49ddd-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ddd-125">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="49ddd-127">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="49ddd-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="49ddd-128">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="49ddd-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicaciones][2]

4. <span data-ttu-id="49ddd-130">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="49ddd-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicaciones][3]

5. <span data-ttu-id="49ddd-132">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicaciones][4]

6. <span data-ttu-id="49ddd-134">En el cuadro de búsqueda de hello, escriba **SilkRoad vida Suite**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Aplicaciones][5]

7. <span data-ttu-id="49ddd-136">En el panel de resultados de hello, seleccione **SilkRoad vida Suite**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="49ddd-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplicaciones][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="49ddd-138">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ddd-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="49ddd-139">objetivo de Hola de esta sección es tooshow cómo tooconfigure y prueba de Azure AD SSO con SilkRoad vida Suite a partir de un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="49ddd-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49ddd-140">Para toowork SSO, Azure AD necesita tooknow es qué usuario equivalente de hello en usuario de tooan SilkRoad vida Suite en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49ddd-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="49ddd-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SilkRoad vida Suite debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="49ddd-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="49ddd-142">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en SilkRoad vida Suite.</span><span class="sxs-lookup"><span data-stu-id="49ddd-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="49ddd-143">tooconfigure y prueba de inicio de sesión único en Azure AD con SilkRoad vida Suite, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="49ddd-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49ddd-144">**[Configuración del inicio de sesión único en Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="49ddd-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49ddd-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="49ddd-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49ddd-146">**[Crear un usuario de prueba del conjunto de vida de SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave un equivalente de Britta Simon SilkRoad vida conjunto de representación toohello vinculado Azure AD de ella.</span><span class="sxs-lookup"><span data-stu-id="49ddd-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="49ddd-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="49ddd-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49ddd-148">**[Probar el inicio de sesión único](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="49ddd-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="49ddd-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ddd-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="49ddd-150">objetivo de Hola de esta sección es tooenable Azure AD SSO en el portal de Azure clásico de Hola y tooconfigure SSO en la aplicación SilkRoad vida Suite.</span><span class="sxs-lookup"><span data-stu-id="49ddd-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="49ddd-151">**tooconfigure inicio de sesión único en Azure AD con SilkRoad vida Suite, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="49ddd-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ddd-152">Sitio de empresa de SilkRoad tooyour de inicio de sesión como administrador.</span><span class="sxs-lookup"><span data-stu-id="49ddd-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="49ddd-153">tooobtain acceso toohello autenticación de conjunto de vida de SilkRoad de aplicación para configurar la federación con Microsoft Azure AD, póngase en contacto con soporte técnico de SilkRoad o con su representante de servicios de SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="49ddd-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="49ddd-154">Vaya demasiado**proveedor de servicios**y, a continuación, haga clic en **detalles de la federación**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][10] 

3. <span data-ttu-id="49ddd-156">Haga clic en **descargar metadatos de federación**y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="49ddd-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Inicio de sesión único de Azure AD ][11] 

4. <span data-ttu-id="49ddd-158">En el portal de Azure clásico en Hola Hola **SilkRoad vida Suite** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar Single Sign-On**  cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="49ddd-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][6] 

5. <span data-ttu-id="49ddd-160">En hello **¿cómo desea que los usuarios toosign en tooSilkRoad Suite de vida** página, seleccione **Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][7] 

6. <span data-ttu-id="49ddd-162">En hello **configurar opciones de aplicación** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="49ddd-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Inicio de sesión único de Azure AD ][8]   
 1. <span data-ttu-id="49ddd-164">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por el sitio de los usuarios en toosign tooyour SilkRoad vida Suite (p. ej.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="49ddd-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="49ddd-165">Abra Hola descargado **Silkroad** archivo de metadatos.</span><span class="sxs-lookup"><span data-stu-id="49ddd-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="49ddd-166">Busque hello **AssertionConsumerService** etiqueta y, a continuación, Hola copia **ubicación** atributo.</span><span class="sxs-lookup"><span data-stu-id="49ddd-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Inicio de sesión único de Azure AD ][21] 
 4. <span data-ttu-id="49ddd-168">Pegue el valor de hello en hello **dirección URL de respuesta** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="49ddd-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="49ddd-169">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-169">Click **Next**.</span></span>

6. <span data-ttu-id="49ddd-170">En hello **configurar inicio de sesión único en el conjunto de vida de SilkRoad** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="49ddd-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Inicio de sesión único de Azure AD ][9]  
 1. <span data-ttu-id="49ddd-172">Haga clic en Descargar certificado y, a continuación, guarde el archivo hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="49ddd-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="49ddd-173">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-173">Click **Next**.</span></span>

7. <span data-ttu-id="49ddd-174">En la aplicación **SilkRoad**, haga clic en **Authentication Sources** (Orígenes de autenticación).</span><span class="sxs-lookup"><span data-stu-id="49ddd-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][12] 

8. <span data-ttu-id="49ddd-176">Haga clic en **Add Authentication Source**(Agregar origen de autenticación).</span><span class="sxs-lookup"><span data-stu-id="49ddd-176">Click **Add Authentication Source**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][13] 

9. <span data-ttu-id="49ddd-178">Hola **agregar origen de autenticación** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="49ddd-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Inicio de sesión único de Azure AD ][14]  
 1. <span data-ttu-id="49ddd-180">En **opción 2: archivo de metadatos**, haga clic en **examinar** hello tooupload descargado el archivo de metadatos.</span><span class="sxs-lookup"><span data-stu-id="49ddd-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="49ddd-181">Haga clic en **Create Identity Provider using File Data**(Crear proveedor de identidades con los datos del archivo).</span><span class="sxs-lookup"><span data-stu-id="49ddd-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="49ddd-182">Hola **fuentes de autenticación** sección, haga clic en **editar**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Inicio de sesión único de Azure AD ][15] 

11. <span data-ttu-id="49ddd-184">En hello **Editar origen de autenticación** cuadro de diálogo, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="49ddd-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Inicio de sesión único de Azure AD ][16] 
 1. <span data-ttu-id="49ddd-186">En **Enabled** (Habilitado), seleccione **Yes** (Sí).</span><span class="sxs-lookup"><span data-stu-id="49ddd-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="49ddd-187">Hola **IdP descripción** cuadro de texto, escriba una descripción para la configuración (p. ej.: *SSO de Azure AD*).</span><span class="sxs-lookup"><span data-stu-id="49ddd-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="49ddd-188">Hola **nombre IdP** cuadro de texto, escriba un nombre de configuración específico tooyour (p. ej.: *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="49ddd-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="49ddd-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-189">Click **Save**.</span></span>

12. <span data-ttu-id="49ddd-190">Deshabilite todos los demás orígenes de autenticación.</span><span class="sxs-lookup"><span data-stu-id="49ddd-190">Disable all other authentication sources.</span></span> 
    
     ![Inicio de sesión único de Azure AD ][17]

13. <span data-ttu-id="49ddd-192">En el portal de Azure clásico en Hola Hola **única confirmación de inicio de sesión** página, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Inicio de sesión único de Azure AD ][18]

14. <span data-ttu-id="49ddd-194">En hello **única confirmación de inicio de sesión** página, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Inicio de sesión único de Azure AD ][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="49ddd-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ddd-196">Create an Azure AD test user</span></span>
<span data-ttu-id="49ddd-197">objetivo de Hola de esta sección es un usuario de prueba en el portal de Azure clásico que se llama a Britta Simon hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="49ddd-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="49ddd-199">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="49ddd-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ddd-200">Hola **portal de Azure clásico**, en Hola panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="49ddd-202">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="49ddd-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="49ddd-203">Haga clic en lista de hello toodisplay de usuarios, en el menú de hello en la parte superior de hello, **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49ddd-205">Hola tooopen **Agregar usuario** cuadro de diálogo, en la barra de herramientas de hello en la parte inferior de hello, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="49ddd-207">En hello **envíenos comentarios acerca de este usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="49ddd-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="49ddd-209">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="49ddd-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="49ddd-210">En nombre de usuario de hello **cuadro de texto**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="49ddd-211">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-211">Click **Next**.</span></span>

6. <span data-ttu-id="49ddd-212">En hello **perfil de usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="49ddd-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="49ddd-214">Hola **nombre** cuadro de texto, tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="49ddd-215">Hola **Last Name** cuadro de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="49ddd-216">Hola **nombre para mostrar** cuadro de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="49ddd-217">Hola **rol** lista, seleccione **usuario**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="49ddd-218">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-218">Click **Next**.</span></span>

7. <span data-ttu-id="49ddd-219">En hello **obtener contraseña temporal** página del cuadro de diálogo, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="49ddd-221">En hello **obtener contraseña temporal** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="49ddd-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="49ddd-223">Anote el valor de Hola de hello **nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="49ddd-224">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="49ddd-225">Creación de un usuario de prueba de SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="49ddd-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="49ddd-226">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en conjunto de vida de SilkRoad toocreate.</span><span class="sxs-lookup"><span data-stu-id="49ddd-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="49ddd-227">Bárbara debe tener un Id. de SSO (a veces denominado tooas una *AuthParam*) que coincide con la de Bárbara **emailaddress** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49ddd-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="49ddd-228">**toocreate un usuario llamado Britta Simon en conjunto de vida SilkRoad, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="49ddd-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="49ddd-229">Solicite a su toocreate de equipo de soporte técnico de SilkRoad vida Suite un usuario que tenga como **Id. de SSO** Hola atributo mismo valor que hello **emailaddress** de Britta Simon en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49ddd-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="49ddd-230">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="49ddd-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="49ddd-231">objetivo de Hola de esta sección es tooenable Britta Simon toouse Azure SSO mediante la concesión de su conjunto de vida de tooSilkRoad de acceso.</span><span class="sxs-lookup"><span data-stu-id="49ddd-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="49ddd-233">**tooassign Britta Simon tooSilkRoad Suite de vida, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="49ddd-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="49ddd-234">En hello Azure portal clásico, vista de aplicaciones de hello tooopen, en la vista de directorio de hello, haga clic en **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="49ddd-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Asignar usuario][201] 

2. <span data-ttu-id="49ddd-236">En la lista de aplicaciones de hello, seleccione **SilkRoad vida Suite**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Asignar usuario][202] 

3. <span data-ttu-id="49ddd-238">En el menú de hello en la parte superior de hello, haga clic en **usuarios**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Asignar usuario][203] 

4. <span data-ttu-id="49ddd-240">En la lista de usuarios de hello, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="49ddd-241">En la barra de herramientas de hello en la parte inferior de hello, haga clic en **asignar**.</span><span class="sxs-lookup"><span data-stu-id="49ddd-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="49ddd-243">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="49ddd-243">Test single sign-on</span></span>
<span data-ttu-id="49ddd-244">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="49ddd-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="49ddd-245">Al hacer clic en icono de conjunto de vida SilkRoad Hola Hola Panel de acceso, deberá obtener la aplicación de conjunto de vida de SilkRoad tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="49ddd-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49ddd-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="49ddd-246">Additional Resources</span></span>
* [<span data-ttu-id="49ddd-247">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49ddd-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49ddd-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49ddd-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





