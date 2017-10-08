---
title: "Tutorial: Integración de Azure Active Directory con Absorb LMS | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y absorber LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="9cf07-103">Tutorial: Integración de Azure Active Directory con Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="9cf07-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="9cf07-104">En este tutorial, aprenderá cómo toointegrate absorber LMS con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cf07-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cf07-105">Integración absorber LMS con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="9cf07-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cf07-106">Puede controlar en Azure AD que tenga acceso tooAbsorb LMS</span><span class="sxs-lookup"><span data-stu-id="9cf07-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="9cf07-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooAbsorb LMS (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf07-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cf07-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9cf07-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9cf07-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte.</span><span class="sxs-lookup"><span data-stu-id="9cf07-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9cf07-110">[¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="9cf07-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cf07-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9cf07-111">Prerequisites</span></span>

<span data-ttu-id="9cf07-112">integración de Azure AD con LMS absorber tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="9cf07-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="9cf07-113">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf07-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9cf07-114">Una suscripción habilitada para inicio de sesión único en Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="9cf07-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cf07-115">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9cf07-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cf07-116">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="9cf07-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cf07-117">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9cf07-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cf07-118">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cf07-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cf07-119">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="9cf07-119">Scenario description</span></span>
<span data-ttu-id="9cf07-120">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="9cf07-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cf07-121">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="9cf07-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cf07-122">Agregar absorber LMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9cf07-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="9cf07-123">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf07-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="9cf07-124">Agregar absorber LMS desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="9cf07-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="9cf07-125">integración de hello tooconfigure de absorber LMS en tooAzure AD, deberá tooadd absorber LMS de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="9cf07-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cf07-126">**tooadd absorber LMS de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf07-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf07-127">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9cf07-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="9cf07-129">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cf07-130">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-130">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="9cf07-132">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf07-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="9cf07-134">En el cuadro de búsqueda de hello, escriba **absorber LMS**, seleccione **absorber LMS** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cf07-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Absorber LMS en la lista de resultados de Hola](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9cf07-136">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf07-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9cf07-137">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Absorb LMS con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9cf07-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9cf07-138">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en LMS absorber es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cf07-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="9cf07-139">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en LMS absorber debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="9cf07-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="9cf07-140">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** en absorber LMS.</span><span class="sxs-lookup"><span data-stu-id="9cf07-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="9cf07-141">tooconfigure y prueba de inicio de sesión único en Azure AD con LMS absorber, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="9cf07-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cf07-142">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="9cf07-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cf07-143">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cf07-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cf07-144">**[Crear un usuario de prueba de absorber LMS](#create-an-absorb-lms-test-user)**  -toohave un equivalente de Britta Simon en LMS absorber que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="9cf07-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cf07-145">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9cf07-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cf07-146">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="9cf07-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9cf07-147">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf07-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9cf07-148">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de absorber LMS.</span><span class="sxs-lookup"><span data-stu-id="9cf07-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="9cf07-149">**inicio de sesión único en tooconfigure Azure AD con LMS absorber, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf07-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf07-150">En el portal de Azure, en Hola Hola **absorber LMS** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="9cf07-152">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="9cf07-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="9cf07-154">En hello **absorber LMS dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="9cf07-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="9cf07-156">a.</span><span class="sxs-lookup"><span data-stu-id="9cf07-156">a.</span></span> <span data-ttu-id="9cf07-157">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="9cf07-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="9cf07-158">b.</span><span class="sxs-lookup"><span data-stu-id="9cf07-158">b.</span></span> <span data-ttu-id="9cf07-159">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="9cf07-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="9cf07-160">Estos valores no son Hola real.</span><span class="sxs-lookup"><span data-stu-id="9cf07-160">These values are not hello real.</span></span> <span data-ttu-id="9cf07-161">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="9cf07-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9cf07-162">Póngase en contacto con [equipo de soporte técnico de absorber LMS cliente](https://www.absorblms.com/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="9cf07-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="9cf07-163">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="9cf07-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="9cf07-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="9cf07-165">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="9cf07-167">En hello **absorber la configuración de LMS** sección, haga clic en **configurar LMS absorber** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="9cf07-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9cf07-168">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="9cf07-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="9cf07-170">En una ventana del explorador web diferente, inicie sesión en el sitio de la compañía absorber LMS tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="9cf07-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="9cf07-171">Haga clic en hello **icono de cuenta** en la interfaz de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf07-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="9cf07-173">Haga clic en **Portal Settings** (Configuración del portal).</span><span class="sxs-lookup"><span data-stu-id="9cf07-173">Click **Portal Settings**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="9cf07-175">Haga clic en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="9cf07-175">Click hello **Users** tab.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="9cf07-177">Lleve a cabo Hola siguiendo los pasos tooaccess Hola Single Sign-On campos de la configuración:</span><span class="sxs-lookup"><span data-stu-id="9cf07-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="9cf07-179">a.</span><span class="sxs-lookup"><span data-stu-id="9cf07-179">a.</span></span> <span data-ttu-id="9cf07-180">Seleccione Hola adecuado **modo**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="9cf07-181">b.</span><span class="sxs-lookup"><span data-stu-id="9cf07-181">b.</span></span> <span data-ttu-id="9cf07-182">Hola abierto certificado que ha descargado de hello portal de Azure en el Bloc de notas, quite hello **---BEGIN CERTIFICATE---** y **---END CERTIFICATE---** etiqueta y, a continuación, pegue Hola restantes contenido en Hola **clave** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="9cf07-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="9cf07-183">c.</span><span class="sxs-lookup"><span data-stu-id="9cf07-183">c.</span></span> <span data-ttu-id="9cf07-184">Hola **propiedad Id**, seleccione Hola atributo apropiado de que ha configurado como Hola identificador de usuario en hello Azure AD (por ejemplo, si se selecciona userprinciplename hello en Azure AD, nombre de usuario se seleccionará aquí.)</span><span class="sxs-lookup"><span data-stu-id="9cf07-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="9cf07-185">d.</span><span class="sxs-lookup"><span data-stu-id="9cf07-185">d.</span></span> <span data-ttu-id="9cf07-186">Hola **dirección URL de inicio de sesión**, pegue hello **"SAML Single Sign-On dirección URL del servicio"** valor haya copiado desde hello **configurar inicio de sesión** ventana de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf07-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="9cf07-187">e.</span><span class="sxs-lookup"><span data-stu-id="9cf07-187">e.</span></span> <span data-ttu-id="9cf07-188">Hola **Logout URL**, pegue hello **"URL de cierre de sesión"** valor haya copiado desde hello **configurar inicio de sesión** ventana de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf07-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="9cf07-189">Habilite **"Only Allow SSO Login"** (Solo permitir inicio de sesión SSO).</span><span class="sxs-lookup"><span data-stu-id="9cf07-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="9cf07-191">Haga clic en **"Save"** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="9cf07-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="9cf07-192">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="9cf07-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9cf07-193">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf07-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9cf07-194">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cf07-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9cf07-195">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf07-195">Create an Azure AD test user</span></span>

<span data-ttu-id="9cf07-196">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="9cf07-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="9cf07-198">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf07-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf07-199">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="9cf07-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cf07-201">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cf07-203">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf07-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cf07-205">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9cf07-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cf07-207">a.</span><span class="sxs-lookup"><span data-stu-id="9cf07-207">a.</span></span> <span data-ttu-id="9cf07-208">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cf07-209">b.</span><span class="sxs-lookup"><span data-stu-id="9cf07-209">b.</span></span> <span data-ttu-id="9cf07-210">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cf07-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cf07-211">c.</span><span class="sxs-lookup"><span data-stu-id="9cf07-211">c.</span></span> <span data-ttu-id="9cf07-212">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9cf07-213">d.</span><span class="sxs-lookup"><span data-stu-id="9cf07-213">d.</span></span> <span data-ttu-id="9cf07-214">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="9cf07-215">Creación de un usuario de prueba de Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="9cf07-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="9cf07-216">toolog de los usuarios de Azure AD tooenable en tooAbsorb LMS, se les deben aprovisionar en tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9cf07-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="9cf07-217">En el caso de Absorb LMS, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="9cf07-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="9cf07-218">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf07-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf07-219">Inicie sesión en tooyour sitio absorber LMS de su compañía como administrador.</span><span class="sxs-lookup"><span data-stu-id="9cf07-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="9cf07-220">Haga clic en la pestaña **Users** (Usuarios).</span><span class="sxs-lookup"><span data-stu-id="9cf07-220">Click **Users** tab.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="9cf07-222">Haga clic en **usuarios** en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="9cf07-222">Click **Users** under hello **Users** tab.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="9cf07-224">Seleccione **User** (Usuario) de la lista desplegable **Add New** (Agregar nuevo).</span><span class="sxs-lookup"><span data-stu-id="9cf07-224">Select **User** from **Add New** drop-down.</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="9cf07-226">En hello **Agregar usuario** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="9cf07-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Invitar a contactos](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="9cf07-228">a.</span><span class="sxs-lookup"><span data-stu-id="9cf07-228">a.</span></span> <span data-ttu-id="9cf07-229">Hola **nombre** cuadro de texto Nombre tipo hello como Bárbara.</span><span class="sxs-lookup"><span data-stu-id="9cf07-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="9cf07-230">b.</span><span class="sxs-lookup"><span data-stu-id="9cf07-230">b.</span></span> <span data-ttu-id="9cf07-231">Hola **Last Name** cuadro de texto, escriba Hola apellidos como Simon.</span><span class="sxs-lookup"><span data-stu-id="9cf07-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="9cf07-232">c.</span><span class="sxs-lookup"><span data-stu-id="9cf07-232">c.</span></span> <span data-ttu-id="9cf07-233">Hola **nombre de usuario** cuadro de texto, escriba el nombre de usuario de hello como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cf07-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="9cf07-234">d.</span><span class="sxs-lookup"><span data-stu-id="9cf07-234">d.</span></span> <span data-ttu-id="9cf07-235">Hola **contraseña** cuadro de texto, escriba la contraseña de Britta Simon Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf07-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="9cf07-236">e.</span><span class="sxs-lookup"><span data-stu-id="9cf07-236">e.</span></span> <span data-ttu-id="9cf07-237">Hola **Confirmar contraseña** cuadro de texto, hello tipo misma contraseña.</span><span class="sxs-lookup"><span data-stu-id="9cf07-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="9cf07-238">f.</span><span class="sxs-lookup"><span data-stu-id="9cf07-238">f.</span></span> <span data-ttu-id="9cf07-239">Establézcalo en **ACTIVE** (ACTIVO).</span><span class="sxs-lookup"><span data-stu-id="9cf07-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="9cf07-240">Haga clic en **"Save"** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="9cf07-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9cf07-241">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf07-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9cf07-242">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="9cf07-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Asigne el rol de usuario de Hola][200]

<span data-ttu-id="9cf07-244">**tooassign Britta Simon tooAbsorb LMS, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="9cf07-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf07-245">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="9cf07-247">En la lista de aplicaciones de hello, seleccione **absorber LMS**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![Hola absorber LMS vínculo en la lista de aplicaciones de Hola](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="9cf07-249">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="9cf07-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-251">Click **Add** button.</span></span> <span data-ttu-id="9cf07-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="9cf07-254">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cf07-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cf07-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cf07-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="9cf07-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9cf07-257">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="9cf07-257">Test single sign-on</span></span>

<span data-ttu-id="9cf07-258">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="9cf07-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9cf07-259">Haga clic en hello absorber LMS disponer en mosaico en hello Panel de acceso, obtendrá una aplicación de absorber LMS tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="9cf07-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="9cf07-260">Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9cf07-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cf07-261">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="9cf07-261">Additional resources</span></span>

* [<span data-ttu-id="9cf07-262">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cf07-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cf07-263">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cf07-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

