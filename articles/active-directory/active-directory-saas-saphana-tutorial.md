---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA| Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="34293-103">Tutorial: Integración de Azure Active Directory con SAP HANA</span><span class="sxs-lookup"><span data-stu-id="34293-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="34293-104">En este tutorial, aprenderá cómo toointegrate SAP HANA con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="34293-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34293-105">Integración de SAP HANA con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="34293-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34293-106">Puede controlar en Azure AD que tenga acceso tooSAP HANA</span><span class="sxs-lookup"><span data-stu-id="34293-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="34293-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSAP HANA (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34293-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34293-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="34293-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34293-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34293-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34293-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="34293-110">Prerequisites</span></span>

<span data-ttu-id="34293-111">tooconfigure integración de Azure AD con SAP HANA, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="34293-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="34293-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34293-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34293-113">Una suscripción habilitada para el inicio de sesión único en SAP HANA</span><span class="sxs-lookup"><span data-stu-id="34293-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="34293-114">Instancia HANA en ejecución en cualquier IaaS pública, instancias locales, VM de Azure o instancias grandes de SAP en Azure</span><span class="sxs-lookup"><span data-stu-id="34293-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="34293-115">Hola XSA administración Web Interface, así como Studio HANA instalado en la instancia HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="34293-116">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="34293-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="34293-117">Probar la integración de Hola primero en el desarrollo o el entorno de aplicación hello y, a continuación, entorno de producción de hello de uso de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="34293-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="34293-118">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="34293-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34293-119">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="34293-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34293-120">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34293-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34293-121">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="34293-121">Scenario description</span></span>
<span data-ttu-id="34293-122">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="34293-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34293-123">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="34293-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34293-124">Adición de SAP HANA desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="34293-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="34293-125">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34293-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="34293-126">Adición de SAP HANA desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="34293-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="34293-127">integración de hello tooconfigure de SAP HANA en Azure AD, deberá tooadd SAP HANA en lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="34293-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34293-128">**tooadd SAP HANA desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34293-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34293-129">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="34293-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="34293-131">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="34293-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34293-132">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="34293-132">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="34293-134">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34293-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="34293-136">En el cuadro de búsqueda de hello, escriba **SAP HANA**, seleccione **SAP HANA** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="34293-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Hola nueva aplicación](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34293-138">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34293-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34293-139">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SAP HANA con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="34293-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="34293-140">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en SAP HANA es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34293-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="34293-141">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en SAP HANA debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="34293-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="34293-142">En SAP HANA, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="34293-143">tooconfigure y prueba de inicio de sesión único en Azure AD con SAP HANA, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="34293-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34293-144">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="34293-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34293-145">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34293-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34293-146">**[Crear un usuario de prueba de SAP HANA](#creating-a-sap-hana-test-user) ** -toohave un equivalente de Britta Simon en SAP HANA que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="34293-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34293-147">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="34293-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34293-148">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="34293-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34293-149">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34293-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34293-150">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="34293-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="34293-151">**inicio de sesión único en Azure AD tooconfigure con SAP HANA, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34293-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="34293-152">En el portal de Azure, en Hola Hola **SAP HANA** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="34293-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="34293-154">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="34293-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="34293-156">En hello **SAP HANA dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="34293-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Información sobre dominio y direcciones URL de inicio de sesión único](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="34293-158">a.</span><span class="sxs-lookup"><span data-stu-id="34293-158">a.</span></span> <span data-ttu-id="34293-159">Hola **identificador** cuadro de texto, tipo como:`HA100`</span><span class="sxs-lookup"><span data-stu-id="34293-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="34293-160">b.</span><span class="sxs-lookup"><span data-stu-id="34293-160">b.</span></span> <span data-ttu-id="34293-161">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="34293-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34293-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="34293-162">These values are not real.</span></span> <span data-ttu-id="34293-163">Actualizar estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="34293-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="34293-164">Póngase en contacto con [equipo de soporte técnico de SAP HANA cliente](https://cloudplatform.sap.com/contact.html) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="34293-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="34293-165">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="34293-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="34293-167">Si el certificado no está activo, después, actívelo haciendo clic en hello "hacer nueva certificado active" la casilla de verificación en hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="34293-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="34293-168">Aplicación de SAP HANA espera las aserciones de SAML de hello en un formato concreto.</span><span class="sxs-lookup"><span data-stu-id="34293-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="34293-169">Hola siguiente captura de pantalla muestra un ejemplo de esto.</span><span class="sxs-lookup"><span data-stu-id="34293-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="34293-170">Aquí hemos asignamos hello **identificador de usuario** con **ExtractMailPrefix()** función de **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="34293-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="34293-171">Esto proporciona el valor de prefijo de saludo de correo electrónico del usuario de Hola que es Hola ID de usuario único.</span><span class="sxs-lookup"><span data-stu-id="34293-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="34293-172">Toohello aplicación de SAP HANA, se envía cada respuesta correcta.</span><span class="sxs-lookup"><span data-stu-id="34293-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="34293-174">Hola **atributos de usuario** sección en hello **inicio de sesión único** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="34293-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="34293-175">a.</span><span class="sxs-lookup"><span data-stu-id="34293-175">a.</span></span> <span data-ttu-id="34293-176">Hola **identificador de usuario** lista desplegable, seleccione **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="34293-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="34293-177">b.</span><span class="sxs-lookup"><span data-stu-id="34293-177">b.</span></span> <span data-ttu-id="34293-178">Hola **correo** lista desplegable, seleccione **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="34293-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="34293-179">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="34293-179">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="34293-181">tooconfigure inicio de sesión único en **SAP HANA** lado, inicio de sesión tooyour **consola Web de HANA XSA** examinando toohello respectivo extremo de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="34293-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="34293-182">En la configuración predeterminada de hello, dirección URL de hello redirige pantalla Inicio de sesión de bienvenida solicitud tooa, lo que requiere credenciales de hello autenticado SAP HANA base de datos usuario toocomplete Hola inicio de sesión del proceso de una.</span><span class="sxs-lookup"><span data-stu-id="34293-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="34293-183">usuario de Hola que inicie sesión debe tener tareas de administración de hello privilegios necesarios tooperform SAML.</span><span class="sxs-lookup"><span data-stu-id="34293-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="34293-184">Hola XSA Web Interface, navegue demasiado**proveedor de identidad SAML** y desde allí, haga clic en hello **"+"** -situado en la parte inferior de Hola Hola pantalla toodisplay Hola Agregar identidad proveedor del panel de información y realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="34293-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Agregación del proveedor de identidades](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="34293-186">a.</span><span class="sxs-lookup"><span data-stu-id="34293-186">a.</span></span> <span data-ttu-id="34293-187">Hola **agregar información de proveedor de identidad** panel, pegar Hola contenido de hello Metadata XML, que ha descargado desde el portal de Azure en hello **metadatos** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="34293-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Adición de la configuración del proveedor de identidades](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="34293-189">b.</span><span class="sxs-lookup"><span data-stu-id="34293-189">b.</span></span> <span data-ttu-id="34293-190">Si contenido de hello del documento XML de hello es válido, Hola proceso de análisis extrae tooinsert de la información necesaria de hello en hello **asunto, Id. de entidad y emisor** campos de datos generales de hello área de pantalla y Hola campos de dirección URL de Hola Área de pantalla de destino, por ejemplo, * *dirección URL Base y la dirección URL de SingleSignOn (*)**.</span><span class="sxs-lookup"><span data-stu-id="34293-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Adición de la configuración del proveedor de identidades](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="34293-192">c.</span><span class="sxs-lookup"><span data-stu-id="34293-192">c.</span></span> <span data-ttu-id="34293-193">Área de pantalla en el cuadro de nombre de Hola de hello datos generales, escriba un nombre para el nuevo proveedor de identidades de SSO de SAML Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="34293-194">nombre de Hola de hello SAML IDP es obligatorio y debe ser única; aparece en la lista Hola de IDPs SAML disponibles que se muestra, si selecciona SAML como método de autenticación de Hola para toouse de las aplicaciones de SAP HANA extra, por ejemplo, en área de pantalla de autenticación de Hola de herramienta de administración de artefactos de extra de Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="34293-195">Guardar detalles de Hola de nuevo proveedor de identidades SAML Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="34293-196">Elija **guardar** toosave Hola detalles del proveedor de identidad SAML hello y agregue Hola nueva SAML IDP toohello lista de conocidos IDPs de SAML.</span><span class="sxs-lookup"><span data-stu-id="34293-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![Botón Guardar](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="34293-198">En Studio HANA dentro de las propiedades de sistema de Hola de hello **configuración** ficha, simplemente filtre la configuración por **saml** y ajustar hello **assertion_timeout** de **10 seg.** demasiado**120 segundo**.</span><span class="sxs-lookup"><span data-stu-id="34293-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![assertion_timeout setting](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="34293-200">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="34293-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34293-201">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34293-202">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34293-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34293-203">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="34293-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="34293-204">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="34293-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="34293-206">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34293-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34293-207">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="34293-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34293-209">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="34293-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34293-211">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34293-213">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="34293-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34293-215">a.</span><span class="sxs-lookup"><span data-stu-id="34293-215">a.</span></span> <span data-ttu-id="34293-216">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34293-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34293-217">b.</span><span class="sxs-lookup"><span data-stu-id="34293-217">b.</span></span> <span data-ttu-id="34293-218">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34293-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34293-219">c.</span><span class="sxs-lookup"><span data-stu-id="34293-219">c.</span></span> <span data-ttu-id="34293-220">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="34293-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34293-221">d.</span><span class="sxs-lookup"><span data-stu-id="34293-221">d.</span></span> <span data-ttu-id="34293-222">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="34293-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="34293-223">Creación de un usuario de prueba en SAP HANA</span><span class="sxs-lookup"><span data-stu-id="34293-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="34293-224">toolog de los usuarios de Azure AD tooenable en tooSAP HANA, se les deben aprovisionar en SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="34293-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="34293-225">SAP HANA admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="34293-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="34293-226">Si necesita un usuario toocreate manualmente, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="34293-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="34293-227">Puede cambiar autenticación externa Hola utilizada por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="34293-228">Los usuarios externos se autentican utilizando un sistema externo, por ejemplo un sistema de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="34293-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="34293-229">Para obtener información detallada acerca de las identidades externas, póngase en contacto con su [administrador de dominio](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="34293-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="34293-230">Abra hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) como administrador y habilitar Hola usuario de base de datos de SSO de SAML.</span><span class="sxs-lookup"><span data-stu-id="34293-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![crear usuario](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="34293-232">Graduación Hola casilla invisible toohello a la izquierda de **SAML** y siga el vínculo Configurar el saludo.</span><span class="sxs-lookup"><span data-stu-id="34293-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="34293-233">Haga clic en **agregar** tooadd Hola IDP SAML y haga clic en **Aceptar** seleccionar Hola IDP SAML adecuado.</span><span class="sxs-lookup"><span data-stu-id="34293-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="34293-234">Agregar hello **identidad externa** (p. ej.</span><span class="sxs-lookup"><span data-stu-id="34293-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="34293-235">BrittaSimon aquí) o elija **"Cualquiera"** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="34293-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="34293-236">Si "Cualquiera" casilla no está activada, el nombre de usuario de hello en HANA requiere nombre de Hola de coincidencia de tooexactly del usuario de Hola Hola UPN antes de sufijo de dominio de hello (es decir, BrittaSimon@contoso.com se convertiría en BrittaSimon en HANA).</span><span class="sxs-lookup"><span data-stu-id="34293-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="34293-237">Para realizar pruebas, asigne todos **"XS"** usuario toohello de roles.</span><span class="sxs-lookup"><span data-stu-id="34293-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![Asignación de roles](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="34293-239">Debe conceder solo los permisos adecuados para los casos de uso.</span><span class="sxs-lookup"><span data-stu-id="34293-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="34293-240">Guardar usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34293-241">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="34293-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34293-242">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="34293-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="34293-244">**tooassign Britta Simon tooSAP HANA, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="34293-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="34293-245">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="34293-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="34293-247">En la lista de aplicaciones de hello, seleccione **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="34293-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Asignar usuario](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="34293-249">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="34293-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202] 

4. <span data-ttu-id="34293-251">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="34293-251">Click **Add** button.</span></span> <span data-ttu-id="34293-252">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="34293-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="34293-254">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="34293-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34293-255">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="34293-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34293-256">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="34293-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34293-257">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="34293-257">Testing single sign-on</span></span>

<span data-ttu-id="34293-258">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="34293-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="34293-259">Al hacer clic en icono de SAP HANA Hola Hola Panel de acceso, deberá obtener la aplicación de SAP HANA tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="34293-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="34293-260">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="34293-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34293-261">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="34293-261">Additional resources</span></span>

* [<span data-ttu-id="34293-262">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="34293-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34293-263">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34293-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

