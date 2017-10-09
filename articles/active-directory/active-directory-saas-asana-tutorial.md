---
title: "Tutorial: Integración de Azure Active Directory con Asana | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="8d6e6-103">Tutorial: Integración de Azure Active Directory con Asana</span><span class="sxs-lookup"><span data-stu-id="8d6e6-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="8d6e6-104">En este tutorial, aprenderá cómo toointegrate Asana con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d6e6-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d6e6-105">Integración Asana con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d6e6-106">Puede controlar en Azure AD que tenga acceso tooAsana</span><span class="sxs-lookup"><span data-stu-id="8d6e6-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="8d6e6-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAsana (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e6-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d6e6-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8d6e6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d6e6-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d6e6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d6e6-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8d6e6-110">Prerequisites</span></span>

<span data-ttu-id="8d6e6-111">integración de Azure AD con Asana tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="8d6e6-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d6e6-113">Una suscripción habilitada para el inicio de sesión único en Asana</span><span class="sxs-lookup"><span data-stu-id="8d6e6-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d6e6-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d6e6-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d6e6-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d6e6-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d6e6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d6e6-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="8d6e6-118">Scenario description</span></span>
<span data-ttu-id="8d6e6-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d6e6-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d6e6-121">Agregar Asana desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8d6e6-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="8d6e6-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="8d6e6-123">Agregar Asana desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="8d6e6-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="8d6e6-124">integración de hello tooconfigure de Asana en Azure AD, deberá tooadd Asana de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d6e6-125">**tooadd Asana de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8d6e6-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d6e6-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="8d6e6-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d6e6-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="8d6e6-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="8d6e6-133">En el cuadro de búsqueda de hello, escriba **Asana**, seleccione **Asana** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8d6e6-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8d6e6-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Asana con un usuario de prueba denominado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d6e6-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d6e6-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Asana es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="8d6e6-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Asana debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="8d6e6-139">En Asana, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d6e6-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Asana, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d6e6-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d6e6-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d6e6-143">**[Crear un usuario de prueba Asana](#create-an-asana-test-user)**  -toohave un equivalente de Britta Simon en Asana que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d6e6-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d6e6-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8d6e6-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8d6e6-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Asana.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="8d6e6-148">**inicio de sesión único en Azure AD tooconfigure con Asana, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8d6e6-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d6e6-149">En el portal de Azure, en Hola Hola **Asana** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="8d6e6-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="8d6e6-153">En hello **Asana dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="8d6e6-155">a.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-155">a.</span></span> <span data-ttu-id="8d6e6-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="8d6e6-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="8d6e6-157">b.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-157">b.</span></span> <span data-ttu-id="8d6e6-158">Hola **identificador** cuadro de texto, el valor de tipo:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="8d6e6-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="8d6e6-159">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="8d6e6-161">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="8d6e6-161">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d6e6-163">En hello **Asana configuración** sección, haga clic en **configurar Asana** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8d6e6-164">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="8d6e6-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="8d6e6-166">En otra ventana del explorador, inicio de sesión tooyour Asana aplicación.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="8d6e6-167">tooconfigure SSO en Asana, configuración de área de trabajo de hello acceso haciendo clic en el nombre del área de trabajo de hello en hello superior derecho de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="8d6e6-168">Después, haga clic en la **configuración del \<nombre del área de trabajo\>**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Configuración de SSO de Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="8d6e6-170">En hello **configuración de la organización** ventana, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="8d6e6-171">A continuación, haga clic en **miembros deben iniciar sesión mediante SAMP** configuración de SSO de tooenable Hola.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="8d6e6-172">Hola realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-172">hello perform hello following steps:</span></span>
   
    ![Definición de la configuración de la organización de inicio de sesión único](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="8d6e6-174">a.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-174">a.</span></span> <span data-ttu-id="8d6e6-175">Hola **URL de la página de inicio de sesión** cuadro de texto, pegue hello **SAML Single Sign-On dirección URL del servicio**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="8d6e6-176">b.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-176">b.</span></span> <span data-ttu-id="8d6e6-177">Haga clic en certificado de hello descargado del portal de Azure, a continuación, abrir archivo de certificado de hello mediante el Bloc de notas o el editor de texto preferido.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="8d6e6-178">Copiar el contenido entre Hola Hola comenzar y Hola título del certificado final y péguelo en hello **certificado X.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="8d6e6-179">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-179">Click **Save**.</span></span> <span data-ttu-id="8d6e6-180">Vaya demasiado[Asana guía para configurar SSO](https://asana.com/guide/help/premium/authentication#gl-saml) si necesita más ayuda.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="8d6e6-181">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="8d6e6-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d6e6-182">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d6e6-183">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d6e6-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8d6e6-184">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e6-184">Create an Azure AD test user</span></span>

<span data-ttu-id="8d6e6-185">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="8d6e6-187">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8d6e6-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d6e6-188">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d6e6-190">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d6e6-192">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d6e6-194">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="8d6e6-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d6e6-196">a.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-196">a.</span></span> <span data-ttu-id="8d6e6-197">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d6e6-198">b.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-198">b.</span></span> <span data-ttu-id="8d6e6-199">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d6e6-200">c.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-200">c.</span></span> <span data-ttu-id="8d6e6-201">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d6e6-202">d.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-202">d.</span></span> <span data-ttu-id="8d6e6-203">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="8d6e6-204">Creación de un usuario de prueba de Asana</span><span class="sxs-lookup"><span data-stu-id="8d6e6-204">Create an Asana test user</span></span>

<span data-ttu-id="8d6e6-205">En esta sección, creará un usuario llamado Britta Simon en Asana.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="8d6e6-206">En **Asana**, vaya toohello **equipos** sección en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="8d6e6-207">Botón de signo más haga clic en Hola.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-207">Click hello plus sign button.</span></span> 
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="8d6e6-209">Escriba el correo electrónico de hello britta.simon@contoso.com en Hola cuadro de texto y, a continuación, seleccione **invitar a**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="8d6e6-210">Haga clic en **Enviar invitación**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-210">Click **Send Invite**.</span></span> <span data-ttu-id="8d6e6-211">Hola nuevo usuario recibirá un correo electrónico en su cuenta de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="8d6e6-212">Necesitará toocreate y validar la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8d6e6-213">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d6e6-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8d6e6-214">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAsana.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Asigne el rol de usuario de Hola][200]

<span data-ttu-id="8d6e6-216">**tooassign Britta Simon tooAsana, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="8d6e6-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d6e6-217">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="8d6e6-219">En la lista de aplicaciones de hello, seleccione **Asana**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-219">In hello applications list, select **Asana**.</span></span>

    ![vínculo de Asana Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="8d6e6-221">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="8d6e6-223">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-223">Click **Add** button.</span></span> <span data-ttu-id="8d6e6-224">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="8d6e6-226">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d6e6-227">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d6e6-228">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8d6e6-229">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="8d6e6-229">Test single sign-on</span></span>

<span data-ttu-id="8d6e6-230">objetivo de Hola de esta sección es tootest el inicio de sesión único en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="8d6e6-231">Ir a página de inicio de sesión de tooAsana.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-231">Go tooAsana login page.</span></span> <span data-ttu-id="8d6e6-232">En el cuadro de texto de dirección de correo electrónico de hello, Insertar dirección de correo electrónico de hello britta.simon@contoso.com. Deje el cuadro de texto de hello contraseña en blanco y, a continuación, haga clic en **inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="8d6e6-233">Es posible que la página de inicio de sesión de tooAzure redirigida AD.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="8d6e6-234">Complete sus credenciales de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="8d6e6-235">Ya ha iniciado sesión en Asana.</span><span class="sxs-lookup"><span data-stu-id="8d6e6-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d6e6-236">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="8d6e6-236">Additional resources</span></span>

* [<span data-ttu-id="8d6e6-237">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d6e6-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d6e6-238">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d6e6-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
