---
title: "Tutorial: Integración de Azure Active Directory con SilkRoad Life Suite | Microsoft Docs"
description: "Obtenga información sobre cómo configurar el inicio de sesión único entre Azure Active Directory y SilkRoad Life Suite."
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
ms.openlocfilehash: ecf4e31ecea00d003fc47ea4cebb781ca58957f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="78d2c-103">Tutorial: Integración de Azure Active Directory con SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="78d2c-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="78d2c-104">El objetivo de este tutorial es mostrar cómo integrar SilkRoad Life Suite con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78d2c-104">The objective of this tutorial is to show you how to integrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="78d2c-105">La integración de SilkRoad Life Suite con Azure AD proporciona las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="78d2c-105">Integrating SilkRoad Life Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="78d2c-106">Puede controlar en Azure AD quién tiene acceso a SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="78d2c-106">You can control in Azure AD who has access to SilkRoad Life Suite</span></span> 
* <span data-ttu-id="78d2c-107">Puede permitir que los usuarios inicien sesión automáticamente en SilkRoad Life Suite mediante inicio de sesión único (SSO) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78d2c-107">You can enable your users to automatically get signed-on to SilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="78d2c-108">Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="78d2c-108">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78d2c-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="78d2c-109">Prerequisites</span></span>
<span data-ttu-id="78d2c-110">Para configurar la integración de Azure AD con SilkRoad Life Suite, necesita los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="78d2c-110">To configure Azure AD integration with SilkRoad Life Suite, you need the following items:</span></span>

* <span data-ttu-id="78d2c-111">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78d2c-111">An Azure AD subscription</span></span>
* <span data-ttu-id="78d2c-112">Una suscripción habilitada para el SSO en SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="78d2c-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="78d2c-113">Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="78d2c-113">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="78d2c-114">Para probar los pasos de este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="78d2c-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="78d2c-115">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="78d2c-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="78d2c-116">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78d2c-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="78d2c-117">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="78d2c-117">Scenario Description</span></span>
<span data-ttu-id="78d2c-118">El objetivo de este tutorial es permitirle probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="78d2c-118">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="78d2c-119">La situación descrita en este tutorial consta de dos bloques de creación principales:</span><span class="sxs-lookup"><span data-stu-id="78d2c-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78d2c-120">Adición de SilkRoad Life Suite desde la galería</span><span class="sxs-lookup"><span data-stu-id="78d2c-120">Adding SilkRoad Life Suite from the gallery</span></span> 
2. <span data-ttu-id="78d2c-121">Configuración y prueba del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78d2c-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-the-gallery"></a><span data-ttu-id="78d2c-122">Adición de SilkRoad Life Suite desde la galería</span><span class="sxs-lookup"><span data-stu-id="78d2c-122">Add SilkRoad Life Suite from the gallery</span></span>
<span data-ttu-id="78d2c-123">Para configurar la integración de SilkRoad Life Suite en Azure AD, deberá agregar SilkRoad Life Suite desde la galería a la lista de aplicaciones SaaS administradas.</span><span class="sxs-lookup"><span data-stu-id="78d2c-123">To configure the integration of SilkRoad Life Suite into Azure AD, you need to add SilkRoad Life Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78d2c-124">**Para agregar SilkRoad Life Suite desde la galería, siga estos pasos:**</span><span class="sxs-lookup"><span data-stu-id="78d2c-124">**To add SilkRoad Life Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78d2c-125">En el **Portal de Azure clásico**, en el panel de navegación izquierdo, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-125">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="78d2c-127">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="78d2c-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="78d2c-128">Para abrir la vista de aplicaciones, haga clic en **Applications** , en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="78d2c-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="78d2c-130">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="78d2c-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplicaciones][3]

5. <span data-ttu-id="78d2c-132">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplicaciones][4]

6. <span data-ttu-id="78d2c-134">En el cuadro de búsqueda, escriba **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-134">In the search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Aplicaciones][5]

7. <span data-ttu-id="78d2c-136">En el panel de resultados, seleccione **SilkRoad Life Suite** y, luego, haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78d2c-136">In the results pane, select **SilkRoad Life Suite**, and then click **Complete** to add the application.</span></span>
   
    ![Aplicaciones][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="78d2c-138">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="78d2c-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="78d2c-139">El objetivo de esta sección es mostrar cómo configurar y probar el SSO de Azure AD con SilkRoad Life Suite mediante un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="78d2c-139">The objective of this section is to show you how to configure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78d2c-140">Para que el SSO funcione, Azure AD debe saber cuál es el usuario homólogo en SilkRoad Life Suite de un usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78d2c-140">For SSO to work, Azure AD needs to know what the counterpart user in SilkRoad Life Suite to an user in Azure AD is.</span></span> <span data-ttu-id="78d2c-141">Es decir, hay que establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="78d2c-141">In other words, a link relationship between an Azure AD user and the related user in SilkRoad Life Suite needs to be established.</span></span>

<span data-ttu-id="78d2c-142">Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="78d2c-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="78d2c-143">Para configurar y probar el inicio de sesión único de Azure AD con SilkRoad Life Suite, es preciso completar los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="78d2c-143">To configure and test Azure AD single sign-on with SilkRoad Life Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78d2c-144">**[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on)**: para permitir a los usuarios usar esta característica.</span><span class="sxs-lookup"><span data-stu-id="78d2c-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78d2c-145">**[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78d2c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78d2c-146">**[Creación de un usuario de prueba de SilkRoad Life Suite](#creating-a-silkroad-life-suite-test-user)** : para tener un homólogo de Britta Simon en SilkRoad Life Suite que esté vinculado a la representación de ella en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78d2c-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - to have a counterpart of Britta Simon in SilkRoad Life Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="78d2c-147">**[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78d2c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78d2c-148">**[Prueba del inicio de sesión único](#testing-single-sign-on)**: para comprobar si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="78d2c-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="78d2c-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78d2c-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="78d2c-150">El objetivo de esta sección es habilitar el SSO de Azure AD en el Portal de Azure clásico y configurarlo en la aplicación SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="78d2c-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="78d2c-151">**Para configurar el inicio de sesión único de Azure AD con SilkRoad Life Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="78d2c-151">**To configure Azure AD single sign-on with SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="78d2c-152">Inicie sesión en su sitio de la compañía de SilkRoad Life Suite como administrador.</span><span class="sxs-lookup"><span data-stu-id="78d2c-152">Sign-on to your SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="78d2c-153">Para obtener acceso a la aplicación de autenticación de SilkRoad Life Suite para configurar la federación con Microsoft Azure AD, póngase en contacto con el soporte técnico o el representante de servicios de SilkRoad.</span><span class="sxs-lookup"><span data-stu-id="78d2c-153">To obtain access to the SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="78d2c-154">Vaya a **Proveedor de servicios** y, luego, haga clic en **Detalles de federación**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-154">Go to **Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Inicio de sesión único de Azure AD ][10] 

3. <span data-ttu-id="78d2c-156">Haga clic en **Download Federation Metadata** (Descargar los metadatos de federación). Después, guarde el archivo de metadatos en el equipo.</span><span class="sxs-lookup"><span data-stu-id="78d2c-156">Click **Download Federation Metadata**, and then save the metadata file on your computer.</span></span>
   
    ![Inicio de sesión único de Azure AD ][11] 

4. <span data-ttu-id="78d2c-158">En el Portal de Azure clásico, en la página de integración de aplicaciones de **SilkRoad Life Suite**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-158">In the Azure classic portal, on the **SilkRoad Life Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar inicio de sesión único][6] 

5. <span data-ttu-id="78d2c-160">En la página **¿Cómo desea que los usuarios inicien sesión en SilkRoad Life Suite?**, seleccione **Inicio de sesión único de Azure AD** y, luego, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-160">On the **How would you like users to sign on to SilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][7] 

6. <span data-ttu-id="78d2c-162">En la página de diálogo **Configurar las opciones de la aplicación** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78d2c-162">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Inicio de sesión único de Azure AD ][8]   
 1. <span data-ttu-id="78d2c-164">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL que los usuarios usan para iniciar sesión en el sitio de SilkRoad Life Suite (por ejemplo: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="78d2c-164">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="78d2c-165">Abra el archivo de metadatos **Silkroad** descargado.</span><span class="sxs-lookup"><span data-stu-id="78d2c-165">Open the downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="78d2c-166">Busque la etiqueta **AssertionConsumerService** y, después, copie el atributo **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-166">Locate the **AssertionConsumerService** tag, and then copy the **Location** attribute.</span></span>         
   
    ![Inicio de sesión único de Azure AD ][21] 
 4. <span data-ttu-id="78d2c-168">Pegue el valor en el cuadro de texto **Dirección URL de respuesta** .</span><span class="sxs-lookup"><span data-stu-id="78d2c-168">Paste the value into the **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="78d2c-169">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-169">Click **Next**.</span></span>

6. <span data-ttu-id="78d2c-170">En la página **Configurar inicio de sesión único en SilkRoad Life Suite** , siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="78d2c-170">On the **Configure single sign-on at SilkRoad Life Suite** page, perform the following steps:</span></span>
   
    ![Inicio de sesión único de Azure AD ][9]  
 1. <span data-ttu-id="78d2c-172">Haga clic en Descargar certificado y después guarde el archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="78d2c-172">Click Download certificate, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="78d2c-173">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-173">Click **Next**.</span></span>

7. <span data-ttu-id="78d2c-174">En la aplicación **SilkRoad**, haga clic en **Authentication Sources** (Orígenes de autenticación).</span><span class="sxs-lookup"><span data-stu-id="78d2c-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Inicio de sesión único de Azure AD ][12] 

8. <span data-ttu-id="78d2c-176">Haga clic en **Add Authentication Source**(Agregar origen de autenticación).</span><span class="sxs-lookup"><span data-stu-id="78d2c-176">Click **Add Authentication Source**.</span></span> 
   
    ![Inicio de sesión único de Azure AD][13] 

9. <span data-ttu-id="78d2c-178">En la sección **Add Authentication Source** (Agregar origen de autenticación), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="78d2c-178">In the **Add Authentication Source** section, perform the following steps:</span></span> 
   
    ![Inicio de sesión único de Azure AD ][14]  
 1. <span data-ttu-id="78d2c-180">En **Option 2 - Metadata File** (Opción 2 - Archivo de metadatos), haga clic en **Browse** (Examinar) para cargar el archivo de metadatos descargado.</span><span class="sxs-lookup"><span data-stu-id="78d2c-180">Under **Option 2 - Metadata File**, click **Browse** to upload the downloaded metadata file.</span></span>  
 2. <span data-ttu-id="78d2c-181">Haga clic en **Create Identity Provider using File Data**(Crear proveedor de identidades con los datos del archivo).</span><span class="sxs-lookup"><span data-stu-id="78d2c-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="78d2c-182">En la sección **Authentication Sources** (Orígenes de autenticación), haga clic en **Edit** (Editar).</span><span class="sxs-lookup"><span data-stu-id="78d2c-182">In the **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Inicio de sesión único de Azure AD ][15] 

11. <span data-ttu-id="78d2c-184">En el cuadro de diálogo **Edit Authentication Source** (Editar origen de autenticación), realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="78d2c-184">On the **Edit Authentication Source** dialog, perform the following steps:</span></span> 
    
     ![Inicio de sesión único de Azure AD ][16] 
 1. <span data-ttu-id="78d2c-186">En **Enabled** (Habilitado), seleccione **Yes** (Sí).</span><span class="sxs-lookup"><span data-stu-id="78d2c-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="78d2c-187">En el cuadro de texto **IdP Description** (Descripción de IdP), escriba una descripción para la configuración (por ejemplo, *SSO de Azure AD*).</span><span class="sxs-lookup"><span data-stu-id="78d2c-187">In the **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="78d2c-188">En el cuadro de texto **IdP Name** (Nombre de IdP), escriba un nombre que sea específico para su configuración (por ejemplo, *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="78d2c-188">In the **IdP Name** textbox, type a name that is specific to your configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="78d2c-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-189">Click **Save**.</span></span>

12. <span data-ttu-id="78d2c-190">Deshabilite todos los demás orígenes de autenticación.</span><span class="sxs-lookup"><span data-stu-id="78d2c-190">Disable all other authentication sources.</span></span> 
    
     ![Inicio de sesión único de Azure AD ][17]

13. <span data-ttu-id="78d2c-192">En el Portal de Azure clásico, en la página **Confirmación del inicio de sesión único**, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-192">In the Azure classic portal, on the **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Inicio de sesión único de Azure AD ][18]

14. <span data-ttu-id="78d2c-194">En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Inicio de sesión único de Azure AD ][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="78d2c-196">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78d2c-196">Create an Azure AD test user</span></span>
<span data-ttu-id="78d2c-197">El objetivo de esta sección es crear un usuario de prueba en el Portal de Azure clásico llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="78d2c-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][20]

<span data-ttu-id="78d2c-199">**Siga estos pasos para crear un usuario de prueba en Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="78d2c-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78d2c-200">En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-200">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="78d2c-202">En la lista **Directory** , seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="78d2c-202">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="78d2c-203">Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-203">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78d2c-205">Para abrir el cuadro de diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-205">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="78d2c-207">En la página de diálogo **Proporcione información sobre este usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78d2c-207">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="78d2c-209">En Tipo de usuario, seleccione Nuevo usuario de la organización.</span><span class="sxs-lookup"><span data-stu-id="78d2c-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="78d2c-210">En el cuadro de texto **Nombre de usuario**, escriba**BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-210">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="78d2c-211">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-211">Click **Next**.</span></span>

6. <span data-ttu-id="78d2c-212">En la página de diálogo **Perfil de usuario** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78d2c-212">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="78d2c-214">En el cuadro de texto **Nombre**, escriba **Britta**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-214">In the **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="78d2c-215">En el cuadro de texto **Apellidos**, escriba **Simon**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-215">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="78d2c-216">En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-216">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="78d2c-217">En la lista **Rol**, seleccione **Usuario**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-217">In the **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="78d2c-218">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-218">Click **Next**.</span></span>

7. <span data-ttu-id="78d2c-219">En el cuadro de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-219">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="78d2c-221">En la página de diálogo **Obtener contraseña temporal** , realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="78d2c-221">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="78d2c-223">Anote el valor del campo **Nueva contraseña**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-223">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="78d2c-224">Haga clic en **Completo**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="78d2c-225">Creación de un usuario de prueba de SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="78d2c-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="78d2c-226">El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="78d2c-226">The objective of this section is to create a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="78d2c-227">Britta debe tener un Id. de SSO (a veces se conoce como *AuthParam*) que coincida con su valor de **emailaddress** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78d2c-227">Britta's must have an SSO ID (sometimes referred to as an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="78d2c-228">**Para crear un usuario llamado Britta Simon en SilkRoad Life Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="78d2c-228">**To create a user called Britta Simon in SilkRoad Life Suite, perform the following steps:**</span></span>

- <span data-ttu-id="78d2c-229">Pida al equipo de soporte de SilkRoad Life Suite que cree un usuario que tenga como atributo **SSO ID** el mismo valor que el campo **emailaddress** de Britta Simon en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="78d2c-229">Ask your SilkRoad Life Suite support team to create a user that has as **SSO ID** attribute the same value as the **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="78d2c-230">Asignación del usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="78d2c-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="78d2c-231">El objetivo de esta sección es permitir que Britta Simon use el SSO de Azure concediéndole acceso a SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="78d2c-231">The objective of this section is to enable Britta Simon to use Azure SSO by granting her access to SilkRoad Life Suite.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="78d2c-233">**Para asignar Britta Simon a SilkRoad Life Suite, realice los pasos siguientes:**</span><span class="sxs-lookup"><span data-stu-id="78d2c-233">**To assign Britta Simon to SilkRoad Life Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="78d2c-234">En el Portal de Azure clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en la opción **Aplicaciones** del menú superior.</span><span class="sxs-lookup"><span data-stu-id="78d2c-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Asignar usuario][201] 

2. <span data-ttu-id="78d2c-236">En la lista de aplicaciones, seleccione **SilkRoad Life Suite**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-236">In the applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Asignar usuario][202] 

3. <span data-ttu-id="78d2c-238">En el menú de la parte superior, haga clic en **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-238">In the menu on the top, click **Users**.</span></span>
   
    ![Asignar usuario][203] 

4. <span data-ttu-id="78d2c-240">En la lista Usuarios, seleccione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-240">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="78d2c-241">En la barra de herramientas de la parte inferior, haga clic en **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="78d2c-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Asignar usuario][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="78d2c-243">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="78d2c-243">Test single sign-on</span></span>
<span data-ttu-id="78d2c-244">El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="78d2c-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="78d2c-245">Al hacer clic en el icono SilkRoad Life Suite en el panel de acceso, debería iniciar sesión automáticamente en su aplicación de SilkRoad Life Suite.</span><span class="sxs-lookup"><span data-stu-id="78d2c-245">When you click the SilkRoad Life Suite tile in the Access Panel, you should get automatically signed-on to your SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78d2c-246">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="78d2c-246">Additional Resources</span></span>
* [<span data-ttu-id="78d2c-247">Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78d2c-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78d2c-248">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="78d2c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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





