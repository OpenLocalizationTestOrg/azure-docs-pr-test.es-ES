---
title: "Tutorial: Integración de Azure Active Directory con Panopto | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="b1067-103">Tutorial: Integración de Azure Active Directory con Panopto</span><span class="sxs-lookup"><span data-stu-id="b1067-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="b1067-104">En este tutorial, aprenderá cómo toointegrate Panopto con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1067-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1067-105">Integración Panopto con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="b1067-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b1067-106">Puede controlar en Azure AD que tenga acceso tooPanopto</span><span class="sxs-lookup"><span data-stu-id="b1067-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="b1067-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooPanopto (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1067-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1067-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b1067-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b1067-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1067-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1067-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b1067-110">Prerequisites</span></span>

<span data-ttu-id="b1067-111">integración de Azure AD con Panopto tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="b1067-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="b1067-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1067-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1067-113">Una suscripción habilitada para el inicio de sesión único en Panopto</span><span class="sxs-lookup"><span data-stu-id="b1067-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1067-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="b1067-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1067-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="b1067-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1067-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="b1067-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1067-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1067-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1067-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="b1067-118">Scenario description</span></span>
<span data-ttu-id="b1067-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="b1067-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1067-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="b1067-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1067-121">Agregar Panopto desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b1067-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="b1067-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1067-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="b1067-123">Agregar Panopto desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="b1067-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="b1067-124">integración de hello tooconfigure de Panopto en Azure AD, deberá tooadd Panopto de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="b1067-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b1067-125">**tooadd Panopto de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b1067-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1067-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b1067-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1067-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="b1067-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b1067-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b1067-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="b1067-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b1067-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="b1067-133">En el cuadro de búsqueda de hello, escriba **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="b1067-133">In hello search box, type **Panopto**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="b1067-135">En el panel de resultados de hello, seleccione **Panopto**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b1067-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1067-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1067-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b1067-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Panopto con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b1067-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b1067-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Panopto es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1067-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="b1067-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Panopto debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="b1067-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="b1067-141">En Panopto, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1067-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b1067-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Panopto, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="b1067-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b1067-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="b1067-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b1067-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1067-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1067-145">**[Crear un usuario de prueba de Panopto](#creating-a-panopto-test-user)**  -toohave un equivalente de Britta Simon en Panopto que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="b1067-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1067-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b1067-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1067-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="b1067-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1067-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1067-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1067-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Panopto.</span><span class="sxs-lookup"><span data-stu-id="b1067-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="b1067-150">**inicio de sesión único en tooconfigure Azure AD con Panopto, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b1067-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1067-151">En el portal de Azure, en Hola Hola **Panopto** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="b1067-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="b1067-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="b1067-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="b1067-155">En hello **Panopto dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b1067-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="b1067-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="b1067-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b1067-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="b1067-158">This value is not real.</span></span> <span data-ttu-id="b1067-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="b1067-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b1067-160">Póngase en contacto con [equipo de soporte técnico de cliente de Panopto](mailto:support@panopto.com‎) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="b1067-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="b1067-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="b1067-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="b1067-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="b1067-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b1067-165">En hello **configuración de Panopto** sección, haga clic en **configurar Panopto** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="b1067-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b1067-166">Hola copia **Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="b1067-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="b1067-168">En una ventana del explorador web diferente, inicie sesión en el sitio de la empresa Panopto tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="b1067-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="b1067-169">En la barra de herramientas de Hola Hola izquierda, haga clic en **System**y, a continuación, haga clic en **proveedores de identidades**.</span><span class="sxs-lookup"><span data-stu-id="b1067-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="b1067-170">![Sistema](./media/active-directory-saas-panopto-tutorial/ic777670.png "Sistema")</span><span class="sxs-lookup"><span data-stu-id="b1067-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="b1067-171">Haga clic en **Agregar proveedor**.</span><span class="sxs-lookup"><span data-stu-id="b1067-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="b1067-172">![Proveedores de identidades](./media/active-directory-saas-panopto-tutorial/ic777671.png "Proveedores de identidades")</span><span class="sxs-lookup"><span data-stu-id="b1067-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="b1067-173">Hola sección proveedor SAML, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b1067-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b1067-174">![Configuración de SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Configuración de SaaS")</span><span class="sxs-lookup"><span data-stu-id="b1067-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="b1067-175">a.</span><span class="sxs-lookup"><span data-stu-id="b1067-175">a.</span></span> <span data-ttu-id="b1067-176">De hello **tipo de proveedor** lista, seleccione **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="b1067-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="b1067-177">b.</span><span class="sxs-lookup"><span data-stu-id="b1067-177">b.</span></span> <span data-ttu-id="b1067-178">Hola **nombre de instancia** cuadro de texto, escriba un nombre para la instancia de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1067-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="b1067-179">c.</span><span class="sxs-lookup"><span data-stu-id="b1067-179">c.</span></span> <span data-ttu-id="b1067-180">Hola **descripción** cuadro de texto, escriba una descripción detallada.</span><span class="sxs-lookup"><span data-stu-id="b1067-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="b1067-181">d.</span><span class="sxs-lookup"><span data-stu-id="b1067-181">d.</span></span> <span data-ttu-id="b1067-182">En **Url de la página de rebote** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1067-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b1067-183">e.</span><span class="sxs-lookup"><span data-stu-id="b1067-183">e.</span></span> <span data-ttu-id="b1067-184">Hola **emisor** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b1067-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b1067-185">f.</span><span class="sxs-lookup"><span data-stu-id="b1067-185">f.</span></span> <span data-ttu-id="b1067-186">Abra el certificado codificado en base 64, que ha descargado de Azure portal, Hola copia contenido del mismo en el Portapapeles de tooyour, y, a continuación, péguelo toohello **clave pública** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="b1067-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="b1067-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b1067-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b1067-188">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="b1067-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b1067-189">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="b1067-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b1067-190">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1067-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1067-191">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1067-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="b1067-192">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="b1067-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="b1067-194">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b1067-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1067-195">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="b1067-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1067-197">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="b1067-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1067-199">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1067-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1067-201">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="b1067-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1067-203">a.</span><span class="sxs-lookup"><span data-stu-id="b1067-203">a.</span></span> <span data-ttu-id="b1067-204">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1067-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1067-205">b.</span><span class="sxs-lookup"><span data-stu-id="b1067-205">b.</span></span> <span data-ttu-id="b1067-206">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b1067-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1067-207">c.</span><span class="sxs-lookup"><span data-stu-id="b1067-207">c.</span></span> <span data-ttu-id="b1067-208">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="b1067-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b1067-209">d.</span><span class="sxs-lookup"><span data-stu-id="b1067-209">d.</span></span> <span data-ttu-id="b1067-210">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b1067-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="b1067-211">Creación de un usuario de prueba de Panopto</span><span class="sxs-lookup"><span data-stu-id="b1067-211">Creating a Panopto test user</span></span>

<span data-ttu-id="b1067-212">No hay ningún elemento de acción tooconfigure de aprovisionamiento de usuarios tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="b1067-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="b1067-213">Cuando un usuario asignado intenta toolog en tooPanopto mediante el panel de acceso de hello, Panopto comprueba si existe el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1067-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="b1067-214">Si no hay cuentas de usuario disponibles, Panopto crea una automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b1067-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="b1067-215">Puede usar cualquier otra Panopto usuario cuenta herramienta de creación o las API proporcionadas por Panopto tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1067-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b1067-216">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1067-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b1067-217">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="b1067-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="b1067-219">**tooassign Britta Simon tooPanopto, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="b1067-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="b1067-220">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="b1067-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="b1067-222">En la lista de aplicaciones de hello, seleccione **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="b1067-222">In hello applications list, select **Panopto**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="b1067-224">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b1067-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="b1067-226">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="b1067-226">Click **Add** button.</span></span> <span data-ttu-id="b1067-227">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b1067-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="b1067-229">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="b1067-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b1067-230">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="b1067-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1067-231">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="b1067-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1067-232">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="b1067-232">Testing single sign-on</span></span>

<span data-ttu-id="b1067-233">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="b1067-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b1067-234">Al hacer clic en icono de Panopto Hola Hola Panel de acceso, deberá obtener automáticamente la página de inicio de sesión de Panopto aplicación.</span><span class="sxs-lookup"><span data-stu-id="b1067-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="b1067-235">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1067-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1067-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="b1067-236">Additional resources</span></span>

* [<span data-ttu-id="b1067-237">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1067-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1067-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1067-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

