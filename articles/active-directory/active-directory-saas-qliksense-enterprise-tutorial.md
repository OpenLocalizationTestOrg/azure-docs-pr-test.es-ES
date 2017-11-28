---
title: "Tutorial: Integración de Azure Active Directory con Qlik Sense Enterprise | Microsoft Doc"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Qlik sentido empresarial."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="1c76f-103">Tutorial: Integración de Azure Active Directory con Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="1c76f-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="1c76f-104">En este tutorial, aprenderá cómo toointegrate Qlik sentido empresarial con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c76f-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c76f-105">Integración Qlik sentido empresarial con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="1c76f-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c76f-106">Puede controlar en Azure AD que tenga acceso tooQlik sentido empresarial.</span><span class="sxs-lookup"><span data-stu-id="1c76f-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="1c76f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooQlik sentido empresarial (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c76f-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1c76f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c76f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="1c76f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c76f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c76f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1c76f-110">Prerequisites</span></span>

<span data-ttu-id="1c76f-111">tooconfigure integración de Azure AD con Qlik sentido Enterprise, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="1c76f-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="1c76f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c76f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c76f-113">Una suscripción habilitada para el inicio de sesión único en Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="1c76f-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c76f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1c76f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c76f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="1c76f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c76f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1c76f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c76f-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de evaluación de un mes: [Oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c76f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c76f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="1c76f-118">Scenario description</span></span>
<span data-ttu-id="1c76f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="1c76f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c76f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="1c76f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c76f-121">Agregar Qlik sentido empresarial desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1c76f-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="1c76f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c76f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="1c76f-123">Agregar Qlik sentido empresarial desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="1c76f-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="1c76f-124">integración de hello tooconfigure de Qlik sentido Enterprise en Azure AD, deberá tooadd Qlik sentido empresarial de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="1c76f-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c76f-125">**tooadd Qlik sentido empresarial desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1c76f-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c76f-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="1c76f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="1c76f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c76f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="1c76f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c76f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="1c76f-133">En el cuadro de búsqueda de hello, escriba **Qlik sentido Enterprise**, seleccione **Qlik sentido Enterprise** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1c76f-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Qlik sentido empresarial en la lista de resultados de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1c76f-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c76f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1c76f-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Qlik Sense Enterprise utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1c76f-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c76f-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Qlik sentido empresarial es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c76f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="1c76f-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Qlik sentido empresarial debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="1c76f-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="1c76f-139">En las empresas de sentido Qlik, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1c76f-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Qlik sentido empresarial, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="1c76f-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c76f-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="1c76f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c76f-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c76f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c76f-143">**[Crear un usuario de prueba de Enterprise de sentido Qlik](#create-a-qlik-sense-enterprise-test-user) ** -toohave un equivalente de Britta Simon en Qlik sentido empresarial que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="1c76f-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c76f-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1c76f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c76f-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="1c76f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1c76f-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c76f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1c76f-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación empresarial de sentido Qlik.</span><span class="sxs-lookup"><span data-stu-id="1c76f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="1c76f-148">**tooconfigure inicio de sesión único en Azure AD con Qlik sentido Enterprise, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1c76f-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c76f-149">En el portal de Azure, en Hola Hola **Qlik sentido Enterprise** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="1c76f-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1c76f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="1c76f-153">En hello **Qlik sentido empresarial dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1c76f-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="1c76f-155">a.</span><span class="sxs-lookup"><span data-stu-id="1c76f-155">a.</span></span> <span data-ttu-id="1c76f-156">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="1c76f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="1c76f-157">Tenga en cuenta Hola finales barra diagonal al final de Hola de este URI.</span><span class="sxs-lookup"><span data-stu-id="1c76f-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="1c76f-158">ya que es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="1c76f-158">It is required.</span></span>
    
    <span data-ttu-id="1c76f-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c76f-159">b.</span></span> <span data-ttu-id="1c76f-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="1c76f-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="1c76f-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="1c76f-161">These values are not real.</span></span> <span data-ttu-id="1c76f-162">Actualización de estos valores con Hola real dirección URL de inicio de sesión y el identificador, que se explican más adelante en este tutorial o póngase en contacto con [equipo de soporte técnico de cliente de empresa de sentido Qlik](https://www.qlik.com/us/services/support) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="1c76f-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="1c76f-163">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="1c76f-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="1c76f-165">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="1c76f-165">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1c76f-167">Preparar el archivo XML de metadatos de federación de hello por lo que puede cargar ese servidor de sentido tooQlik.</span><span class="sxs-lookup"><span data-stu-id="1c76f-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="1c76f-168">Antes de cargar Hola IdP metadatos toohello server Qlik sentido, archivo hello necesita toobe editar tooremove información tooensure el funcionamiento correcto entre Azure AD y el servidor de Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="1c76f-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="1c76f-170">a.</span><span class="sxs-lookup"><span data-stu-id="1c76f-170">a.</span></span> <span data-ttu-id="1c76f-171">Abra el archivo de FederationMetaData.xml de hello, que ha descargado desde el portal de Azure en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="1c76f-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="1c76f-172">b.</span><span class="sxs-lookup"><span data-stu-id="1c76f-172">b.</span></span> <span data-ttu-id="1c76f-173">Busque el valor de hello **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="1c76f-174">Hay cuatro entradas (dos pares de etiquetas de elementos de apertura y cierre).</span><span class="sxs-lookup"><span data-stu-id="1c76f-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="1c76f-175">c.</span><span class="sxs-lookup"><span data-stu-id="1c76f-175">c.</span></span> <span data-ttu-id="1c76f-176">Eliminar etiquetas de RoleDescriptor de Hola y toda la información en medio de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="1c76f-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="1c76f-177">d.</span><span class="sxs-lookup"><span data-stu-id="1c76f-177">d.</span></span> <span data-ttu-id="1c76f-178">Guarde el archivo de Hola y mantenerlo cercanas para utilizarlo más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="1c76f-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="1c76f-179">Navegue toohello Qlik sentido Qlik Management Console (QMC) como un usuario que puede crear las configuraciones de proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="1c76f-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="1c76f-180">Hola QMC, haga clic en hello **Proxies Virtual** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="1c76f-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="1c76f-182">En la parte inferior de Hola de pantalla de bienvenida, haga clic en hello **crear nuevo** botón.</span><span class="sxs-lookup"><span data-stu-id="1c76f-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="1c76f-184">aparece la pantalla de edición de Hello Virtual proxy.</span><span class="sxs-lookup"><span data-stu-id="1c76f-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="1c76f-185">En hello lado derecho de la pantalla de bienvenida es un menú para hacer visible las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="1c76f-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="1c76f-187">Con la opción de menú de identificación de hello comprueba, escribe la información de identificación de hello para la configuración de proxy de virtual de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="1c76f-189">a.</span><span class="sxs-lookup"><span data-stu-id="1c76f-189">a.</span></span> <span data-ttu-id="1c76f-190">Hola **descripción** campo es un nombre descriptivo para la configuración de proxy virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="1c76f-191">Escriba un valor para este campo.</span><span class="sxs-lookup"><span data-stu-id="1c76f-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="1c76f-192">b.</span><span class="sxs-lookup"><span data-stu-id="1c76f-192">b.</span></span> <span data-ttu-id="1c76f-193">Hola **prefijo** campo identifica de punto de conexión de hello proxy virtual para conectar tooQlik sentido con Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="1c76f-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="1c76f-194">Escriba un nombre de prefijo único para este proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="1c76f-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="1c76f-195">c.</span><span class="sxs-lookup"><span data-stu-id="1c76f-195">c.</span></span> <span data-ttu-id="1c76f-196">**Tiempo de espera de inactividad de sesión (minutos)** Hola tiempo de espera para las conexiones a través de este proxy virtual.</span><span class="sxs-lookup"><span data-stu-id="1c76f-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="1c76f-197">d.</span><span class="sxs-lookup"><span data-stu-id="1c76f-197">d.</span></span> <span data-ttu-id="1c76f-198">Hola **nombre de encabezado de cookie de sesión** es almacenar nombre de cookie de Hola Hola identificador de sesión de hello sesión Qlik sentido un usuario recibe tras la autenticación correcta.</span><span class="sxs-lookup"><span data-stu-id="1c76f-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="1c76f-199">Este nombre debe ser único.</span><span class="sxs-lookup"><span data-stu-id="1c76f-199">This name must be unique.</span></span>

12. <span data-ttu-id="1c76f-200">Haga clic en hello autenticación menú opción toomake visible.</span><span class="sxs-lookup"><span data-stu-id="1c76f-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="1c76f-201">aparece la pantalla de bienvenida la autenticación.</span><span class="sxs-lookup"><span data-stu-id="1c76f-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="1c76f-203">a.</span><span class="sxs-lookup"><span data-stu-id="1c76f-203">a.</span></span> <span data-ttu-id="1c76f-204">Hola **modo de acceso anónimo** desplegable determina si pueden tener acceso a los usuarios anónimos Qlik sentido a través de proxy virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="1c76f-205">opción predeterminada de Hello no es ningún usuario anónimo.</span><span class="sxs-lookup"><span data-stu-id="1c76f-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="1c76f-206">b.</span><span class="sxs-lookup"><span data-stu-id="1c76f-206">b.</span></span> <span data-ttu-id="1c76f-207">Hola **método de autenticación** desplegable determina el esquema Hola Hola autenticación virtual proxy usará.</span><span class="sxs-lookup"><span data-stu-id="1c76f-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="1c76f-208">Seleccione SAML de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="1c76f-209">Como resultado, aparecerán más opciones.</span><span class="sxs-lookup"><span data-stu-id="1c76f-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="1c76f-210">c.</span><span class="sxs-lookup"><span data-stu-id="1c76f-210">c.</span></span> <span data-ttu-id="1c76f-211">Hola **el campo de identificador URI del host SAML**, los usuarios de nombre de host de entrada Hola escribir tooaccess Qlik sentido a través de este proxy virtual SAML.</span><span class="sxs-lookup"><span data-stu-id="1c76f-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="1c76f-212">nombre de host de Hello es uri Hola de hello server Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="1c76f-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="1c76f-213">d.</span><span class="sxs-lookup"><span data-stu-id="1c76f-213">d.</span></span> <span data-ttu-id="1c76f-214">Hola **Id. de entidad SAML**, escriba Hola mismo valor especificado para el campo de identificador URI de host de hello SAML.</span><span class="sxs-lookup"><span data-stu-id="1c76f-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="1c76f-215">e.</span><span class="sxs-lookup"><span data-stu-id="1c76f-215">e.</span></span> <span data-ttu-id="1c76f-216">Hola **metadatos SAML IdP** es archivo hello editado anteriormente en hello **editar los metadatos de federación de la configuración de AD Azure** sección.</span><span class="sxs-lookup"><span data-stu-id="1c76f-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="1c76f-217">**Antes de cargar los metadatos de IdP de hello, archivo hello necesita toobe editar** tooremove información tooensure el funcionamiento correcto entre Azure AD y el servidor de Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="1c76f-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="1c76f-218">**Consulte instrucciones toohello anteriores si tiene el archivo hello aún toobe editar.**</span><span class="sxs-lookup"><span data-stu-id="1c76f-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="1c76f-219">Si se ha editado el archivo hello haga clic en el botón de examinar hello y tooupload de archivo de metadatos editado Hola seleccione Configuración de proxy virtual toohello.</span><span class="sxs-lookup"><span data-stu-id="1c76f-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="1c76f-220">f.</span><span class="sxs-lookup"><span data-stu-id="1c76f-220">f.</span></span> <span data-ttu-id="1c76f-221">Escriba la referencia de esquema o nombre de atributo de Hola para atributo SAML de Hola que representa hello **UserID** Azure AD envía toohello server Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="1c76f-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="1c76f-222">Información de referencia de esquema está disponible en hello Azure aplicación pantallas después de la configuración.</span><span class="sxs-lookup"><span data-stu-id="1c76f-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="1c76f-223">atributo de nombre de hello toouse, escriba `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="1c76f-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="1c76f-224">g.</span><span class="sxs-lookup"><span data-stu-id="1c76f-224">g.</span></span> <span data-ttu-id="1c76f-225">Escriba el valor de Hola para hello **directorio usuario** que será toousers adjunto al realizar la autenticación tooQlik servidor de sentido a través de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c76f-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="1c76f-226">Los valores codificados deben estar entre **corchetes**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="1c76f-227">toouse un atributo que se envían en hello aserción de SAML de Azure AD, escriba el nombre de Hola de atributo hello en este cuadro de texto **sin** corchetes.</span><span class="sxs-lookup"><span data-stu-id="1c76f-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="1c76f-228">h.</span><span class="sxs-lookup"><span data-stu-id="1c76f-228">h.</span></span> <span data-ttu-id="1c76f-229">Hola **algoritmo de firma de SAML** conjuntos hello para la configuración de proxy virtual Hola de firma de certificado de proveedor (en este servidor Qlik sentido mayúscula) de servicio.</span><span class="sxs-lookup"><span data-stu-id="1c76f-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="1c76f-230">Si servidor Qlik sentido utiliza un certificado de confianza que se genera mediante RSA mejorado de Microsoft y proveedor de servicios criptográficos de AES, cambie algoritmo de firma de SAML de hello demasiado**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="1c76f-231">i.</span><span class="sxs-lookup"><span data-stu-id="1c76f-231">i.</span></span> <span data-ttu-id="1c76f-232">Hola sección de asignación de atributo SAML permite atributos adicionales como grupos toobe enviado tooQlik sentido para su uso en las reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="1c76f-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="1c76f-233">Haga clic en hello **equilibrio de carga** toomake de opción de menú que visible.</span><span class="sxs-lookup"><span data-stu-id="1c76f-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="1c76f-234">aparece la pantalla de bienvenida equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="1c76f-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="1c76f-236">Haga clic en hello **Agregar nuevo nodo de servidor** botón nodo seleccione motor o nodos Qlik sentido se envíe con fines de equilibrio de carga de las sesiones toofor y haga clic en hello **agregar** botón.</span><span class="sxs-lookup"><span data-stu-id="1c76f-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="1c76f-238">Haga clic en toomake de opción de menú Opciones avanzadas de hello visible.</span><span class="sxs-lookup"><span data-stu-id="1c76f-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="1c76f-239">aparece la pantalla avanzada de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="1c76f-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="1c76f-241">lista blanca de Hello Host identifica los nombres de host que se aceptan cuando se conecte toohello server Qlik sentido.</span><span class="sxs-lookup"><span data-stu-id="1c76f-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="1c76f-242">**Escriba el nombre de host de hello los usuarios especificarán al conectar el servidor de sentido tooQlik.**</span><span class="sxs-lookup"><span data-stu-id="1c76f-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="1c76f-243">nombre de host de Hello es hello mismo valor que Hola SAML host uri sin Hola https://.</span><span class="sxs-lookup"><span data-stu-id="1c76f-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="1c76f-244">Haga clic en hello **aplicar** botón.</span><span class="sxs-lookup"><span data-stu-id="1c76f-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="1c76f-246">Haga clic en el mensaje de advertencia de hello Aceptar tooaccept que indica los servidores proxy se reiniciará proxy virtual toohello vinculado.</span><span class="sxs-lookup"><span data-stu-id="1c76f-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="1c76f-248">En el lado derecho de Hola de pantalla de bienvenida, aparece el menú de elementos de asociados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="1c76f-249">Haga clic en hello **proxy** opción de menú.</span><span class="sxs-lookup"><span data-stu-id="1c76f-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="1c76f-251">aparece la pantalla de bienvenida proxy.</span><span class="sxs-lookup"><span data-stu-id="1c76f-251">hello proxy screen appears.</span></span>  <span data-ttu-id="1c76f-252">Haga clic en hello **vínculo** botón en hello inferior toolink proxy proxy toohello virtual.</span><span class="sxs-lookup"><span data-stu-id="1c76f-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="1c76f-254">Nodo de proxy de hello SELECT que admitirá esta conexión virtual proxy y haga clic en hello **vínculo** botón.</span><span class="sxs-lookup"><span data-stu-id="1c76f-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="1c76f-255">Después de vincular, proxy Hola se enumerará en servidores proxy asociados.</span><span class="sxs-lookup"><span data-stu-id="1c76f-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="1c76f-258">Después de aproximadamente cinco segundos tooten, Hola mensaje Actualizar QMC aparecerá.</span><span class="sxs-lookup"><span data-stu-id="1c76f-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="1c76f-259">Haga clic en hello **QMC actualizar** botón.</span><span class="sxs-lookup"><span data-stu-id="1c76f-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="1c76f-261">Cuando actualiza hello QMC, haga clic en hello **Virtual proxy** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="1c76f-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="1c76f-262">nueva entrada de proxy virtual SAML Hola se muestra en la tabla de hello en la pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="1c76f-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="1c76f-263">Solo un clic en la entrada de proxy virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="1c76f-265">En la parte inferior de Hola de pantalla de bienvenida, se activará un botón de hello SP descargar metadatos.</span><span class="sxs-lookup"><span data-stu-id="1c76f-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="1c76f-266">Haga clic en hello **SP descargar metadatos** archivo tooa de botón toosave hello metadatos.</span><span class="sxs-lookup"><span data-stu-id="1c76f-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="1c76f-268">Archivo de metadatos de sp de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="1c76f-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="1c76f-269">Observar hello **entityID** hello y entrada **AssertionConsumerService** entrada.</span><span class="sxs-lookup"><span data-stu-id="1c76f-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="1c76f-270">Estos valores son equivalente toohello **identificador** hello y **dirección URL de inicio de sesión** en configuración de la aplicación hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c76f-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="1c76f-271">Pegue estos valores en hello **Qlik sentido empresarial dominio y las direcciones URL** sección de configuración de la aplicación hello Azure AD si no coinciden, a continuación, se debe reemplazar en el Asistente para configuración de aplicación de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="1c76f-273">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="1c76f-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1c76f-274">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1c76f-275">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c76f-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1c76f-276">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c76f-276">Create an Azure AD test user</span></span>
<span data-ttu-id="1c76f-277">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="1c76f-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="1c76f-279">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1c76f-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c76f-280">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="1c76f-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![botón de Hello Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="1c76f-282">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="1c76f-284">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c76f-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![botón de agregar Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="1c76f-286">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="1c76f-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="1c76f-288">a.</span><span class="sxs-lookup"><span data-stu-id="1c76f-288">a.</span></span> <span data-ttu-id="1c76f-289">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="1c76f-290">b.</span><span class="sxs-lookup"><span data-stu-id="1c76f-290">b.</span></span> <span data-ttu-id="1c76f-291">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c76f-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="1c76f-292">c.</span><span class="sxs-lookup"><span data-stu-id="1c76f-292">c.</span></span> <span data-ttu-id="1c76f-293">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="1c76f-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="1c76f-294">d.</span><span class="sxs-lookup"><span data-stu-id="1c76f-294">d.</span></span> <span data-ttu-id="1c76f-295">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="1c76f-296">Creación de un usuario de prueba de Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="1c76f-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="1c76f-297">En esta sección, creará un usuario llamado "Britta Simon" en Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1c76f-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="1c76f-298">Trabajar con [equipo de soporte técnico de cliente de empresa de sentido Qlik](https://www.qlik.com/us/services/support) para agregar usuarios de hello en plataforma de hello Qlik sentido empresarial.</span><span class="sxs-lookup"><span data-stu-id="1c76f-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="1c76f-299">Los usuarios se tienen que crear y activar antes de usar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="1c76f-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1c76f-300">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c76f-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1c76f-301">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooQlik sentido empresarial.</span><span class="sxs-lookup"><span data-stu-id="1c76f-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="1c76f-303">**tooassign Britta Simon tooQlik sentido Enterprise, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="1c76f-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c76f-304">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="1c76f-306">En la lista de aplicaciones de hello, seleccione **Qlik sentido Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![vínculo de Hello Qlik sentido empresarial en la lista de aplicaciones de Hola](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="1c76f-308">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="1c76f-310">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-310">Click **Add** button.</span></span> <span data-ttu-id="1c76f-311">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="1c76f-313">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c76f-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c76f-314">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c76f-315">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="1c76f-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1c76f-316">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="1c76f-316">Test single sign-on</span></span>

<span data-ttu-id="1c76f-317">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="1c76f-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1c76f-318">Al hacer clic en icono de Qlik sentido empresarial Hola Hola Panel de acceso, deberá obtener aplicaciones de Qlik sentido Enterprise tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="1c76f-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1c76f-319">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="1c76f-319">Additional resources</span></span>

* [<span data-ttu-id="1c76f-320">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c76f-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c76f-321">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c76f-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

