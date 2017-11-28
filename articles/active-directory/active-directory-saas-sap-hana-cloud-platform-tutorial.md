---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse plataforma en la nube SAP HANA con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="680ff-103">Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="680ff-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="680ff-104">objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y plataforma en la nube SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="680ff-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="680ff-105">escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="680ff-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="680ff-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="680ff-106">A valid Azure subscription</span></span>
* <span data-ttu-id="680ff-107">Una cuenta de SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="680ff-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="680ff-108">Después de completar este tutorial, Hola usuarios de Azure AD que haya asignado tooSAP plataforma de nube de HANA será capaz de toosingle inicio de sesión en la aplicación hello mediante hello [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="680ff-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="680ff-109">Necesita toodeploy su propia aplicación o suscribirse tooan aplicación en la plataforma de nube SAP HANA tootest de cuenta único inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="680ff-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="680ff-110">En este tutorial, una aplicación se implementa en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="680ff-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="680ff-111">escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="680ff-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="680ff-112">Habilitar la integración de aplicación Hola para plataforma en la nube SAP HANA</span><span class="sxs-lookup"><span data-stu-id="680ff-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="680ff-113">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="680ff-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="680ff-114">Asignar un rol tooa a un usuario</span><span class="sxs-lookup"><span data-stu-id="680ff-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="680ff-115">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="680ff-115">Assigning users</span></span>

<span data-ttu-id="680ff-116">![Escenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="680ff-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="680ff-117">Habilitar la integración de aplicación Hola para plataforma en la nube SAP HANA</span><span class="sxs-lookup"><span data-stu-id="680ff-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="680ff-118">objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para plataforma en la nube SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="680ff-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="680ff-119">**integración de aplicaciones de hello tooenable para la plataforma de nube de SAP HANA, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="680ff-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="680ff-120">Hola Portal de administración de Azure, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="680ff-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="680ff-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="680ff-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="680ff-122">De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.</span><span class="sxs-lookup"><span data-stu-id="680ff-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="680ff-123">Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="680ff-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="680ff-124">![Aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="680ff-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="680ff-125">Haga clic en **agregar** final Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="680ff-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="680ff-126">![Agregar aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="680ff-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="680ff-127">En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.</span><span class="sxs-lookup"><span data-stu-id="680ff-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="680ff-128">![Agregar una aplicación de la galería](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="680ff-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="680ff-129">Hola **cuadro de búsqueda**, tipo **plataforma en la nube SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="680ff-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="680ff-130">![Galería de aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="680ff-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="680ff-131">En el panel de resultados de hello, seleccione **plataforma en la nube SAP HANA**y, a continuación, haga clic en **completar** aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="680ff-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="680ff-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="680ff-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="680ff-133">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="680ff-133">Configure single sign-on</span></span>

<span data-ttu-id="680ff-134">objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooSAP plataforma de nube de HANA con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.</span><span class="sxs-lookup"><span data-stu-id="680ff-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="680ff-135">Como parte de este procedimiento, se le tooupload requiere un inquilino de plataforma en la nube SAP HANA tooyour certificado codificado en base 64.</span><span class="sxs-lookup"><span data-stu-id="680ff-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="680ff-136">Si no está familiarizado con este procedimiento, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="680ff-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="680ff-137">**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="680ff-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="680ff-138">En el portal de Azure clásico en Hola Hola **plataforma en la nube SAP HANA** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único**cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="680ff-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="680ff-139">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="680ff-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="680ff-140">En hello **¿cómo desea que toosign a los usuarios en la plataforma de nube de HANA tooSAP** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="680ff-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="680ff-141">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="680ff-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="680ff-142">En una ventana del explorador web diferente, inicie sesión en toohello cabina de plataforma de nube SAP HANA en https://account. \<host horizontal\>.ondemand.com/cockpit (p. ej.: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="680ff-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="680ff-143">Haga clic en hello **confianza** ficha.</span><span class="sxs-lookup"><span data-stu-id="680ff-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="680ff-144">![Confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Confianza")</span><span class="sxs-lookup"><span data-stu-id="680ff-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="680ff-145">En la sección de administración de confianza, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="680ff-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="680ff-146">![Obtención de metadatos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obtención de metadatos")</span><span class="sxs-lookup"><span data-stu-id="680ff-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="680ff-147">Haga clic en hello **proveedor de servicios Local** ficha.</span><span class="sxs-lookup"><span data-stu-id="680ff-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="680ff-148">Hola toodownload archivo de metadatos de la plataforma en la nube SAP HANA, haga clic en **obtener metadatos**.</span><span class="sxs-lookup"><span data-stu-id="680ff-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="680ff-149">En hello Azure Active portal clásico en hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="680ff-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="680ff-150">![Configurar dirección URL de la aplicación](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="680ff-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="680ff-151">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por su toosign a los usuarios en su **plataforma en la nube SAP HANA** aplicación.</span><span class="sxs-lookup"><span data-stu-id="680ff-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="680ff-152">Se trata de una dirección URL específica de la cuenta de hello de un recurso protegido en la aplicación de la plataforma en la nube SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="680ff-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="680ff-153">Hello dirección URL se basa Hola siguiente patrón: *https://\<applicationName\>\<accountName\>.\< host horizontal\>.ondemand.com/\<ruta de acceso\_a\_protegido\_recursos\>*  (p. ej.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="680ff-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="680ff-154">Se trata de dirección URL de hello en la aplicación de plataforma en la nube SAP HANA que requiere hello tooauthenticate de usuario.</span><span class="sxs-lookup"><span data-stu-id="680ff-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="680ff-155">Abrir archivo de metadatos de plataforma en la nube SAP HANA Hola descargado y, a continuación, busque hello **NS3: assertionconsumerservice** etiqueta.</span><span class="sxs-lookup"><span data-stu-id="680ff-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="680ff-156">Copiar valor de Hola de hello **ubicación** de atributo y, a continuación, péguelo en hello **URL de respuesta de plataforma de nube de SAP HANA** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="680ff-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="680ff-157">En hello **configurar inicio de sesión único en plataforma en la nube SAP HANA** page, toodownload sus metadatos, haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="680ff-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="680ff-158">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="680ff-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="680ff-159">En hello cabina de plataforma de nube de SAP HANA, Hola **proveedor de servicios Local** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="680ff-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="680ff-160">![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Administración de confianza")</span><span class="sxs-lookup"><span data-stu-id="680ff-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="680ff-161">Haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="680ff-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="680ff-162">En **Configuration Type** (Tipo de configuración), seleccione **Custom** (Personalizado).</span><span class="sxs-lookup"><span data-stu-id="680ff-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="680ff-163">Como **nombre del proveedor Local**, deje el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="680ff-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="680ff-164">toogenerate una **clave de firma de** y un **certificado de firma de** par de claves, haga clic en **generar el par de claves**.</span><span class="sxs-lookup"><span data-stu-id="680ff-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="680ff-165">En **Principal Propagation** (Propagación de entidad de seguridad), seleccione **Disabled** (Deshabilitada).</span><span class="sxs-lookup"><span data-stu-id="680ff-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="680ff-166">En **Force Authentication** (Forzar autenticación), seleccione **Disabled** (Deshabilitado).</span><span class="sxs-lookup"><span data-stu-id="680ff-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="680ff-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="680ff-167">Click **Save**.</span></span>

9. <span data-ttu-id="680ff-168">Haga clic en hello **proveedor de identidad de confianza** ficha y, a continuación, haga clic en **Agregar proveedor de identidad de confianza**.</span><span class="sxs-lookup"><span data-stu-id="680ff-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="680ff-169">![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Administración de confianza")</span><span class="sxs-lookup"><span data-stu-id="680ff-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="680ff-170">lista de hello toomanage de proveedores de identidad de confianza, deberá toohave elegido Hola tipo de configuración personalizada en hello sección proveedor de servicio Local.</span><span class="sxs-lookup"><span data-stu-id="680ff-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="680ff-171">Para el tipo de configuración predeterminado, tendrá un toohello de confianza implícita que no puede modificar el servicio de Id. de SAP.</span><span class="sxs-lookup"><span data-stu-id="680ff-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="680ff-172">Para Ninguno, no tiene ninguna configuración de confianza.</span><span class="sxs-lookup"><span data-stu-id="680ff-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="680ff-173">Haga clic en hello **General** ficha y, a continuación, haga clic en **examinar** hello tooupload descargado el archivo de metadatos.</span><span class="sxs-lookup"><span data-stu-id="680ff-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="680ff-174">![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Administración de confianza")</span><span class="sxs-lookup"><span data-stu-id="680ff-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="680ff-175">Después de cargar el archivo de metadatos de hello, valores de hello para **dirección URL de inicio de sesión único**, **dirección URL de cierre de sesión único** y **certificado de firma de** se rellenan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="680ff-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="680ff-176">Haga clic en hello **atributos** ficha.</span><span class="sxs-lookup"><span data-stu-id="680ff-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="680ff-177">En hello **atributos** , realice Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="680ff-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="680ff-178">![Atributos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="680ff-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="680ff-179">Haga clic en **Agregar atributo**y, a continuación, agregue Hola siguientes atributos basados en aserción:</span><span class="sxs-lookup"><span data-stu-id="680ff-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="680ff-180">Atributo de aserción</span><span class="sxs-lookup"><span data-stu-id="680ff-180">Assertion Attribute</span></span> | <span data-ttu-id="680ff-181">Atributo de entidad de seguridad</span><span class="sxs-lookup"><span data-stu-id="680ff-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="680ff-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="680ff-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="680ff-183">firstname</span><span class="sxs-lookup"><span data-stu-id="680ff-183">firstname</span></span> |
    | <span data-ttu-id="680ff-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="680ff-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="680ff-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="680ff-185">lastname</span></span> |
    | <span data-ttu-id="680ff-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="680ff-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="680ff-187">email</span><span class="sxs-lookup"><span data-stu-id="680ff-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="680ff-188">configuración de Hola de hello atributos depende de cómo Hola aplicaciones en HCP se desarrollan, es decir, qué atributos esperan en hello respuesta de SAML y con qué nombre (atributo de entidad de seguridad) tienen acceso a este atributo en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="680ff-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="680ff-189">Hola **atributo Default** Hola captura de pantalla es solo para fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="680ff-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="680ff-190">No es necesario trabajo de escenario de toomake Hola.</span><span class="sxs-lookup"><span data-stu-id="680ff-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="680ff-191">Hola nombres y valores de **atributo de entidad de seguridad** se muestra en hello captura de pantalla dependen de cómo se desarrolla la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="680ff-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="680ff-192">Es posible que la aplicación requiera diferentes asignaciones.</span><span class="sxs-lookup"><span data-stu-id="680ff-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="680ff-193">En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en plataforma en la nube SAP HANA** página de diálogo, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar**.</span><span class="sxs-lookup"><span data-stu-id="680ff-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="680ff-194">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="680ff-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="680ff-195">Grupos basados en aserción</span><span class="sxs-lookup"><span data-stu-id="680ff-195">Assertion-based groups</span></span>
<span data-ttu-id="680ff-196">Como paso opcional, puede configurar grupos basados en aserciones para su proveedor de identidades de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="680ff-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="680ff-197">Uso de grupos en plataforma en la nube SAP HANA permite asignar toodynamically uno o más tooone de los usuarios o más roles en las aplicaciones de la plataforma en la nube SAP HANA, determinado por los valores de los atributos de hello SAML 2.0 aserción.</span><span class="sxs-lookup"><span data-stu-id="680ff-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="680ff-198">Por ejemplo, si hello la aserción contiene el atributo de Hola "*contrato = temporal*", puede que desee todos los grupos de usuarios afectados toobe toohello agregado"*temporal*".</span><span class="sxs-lookup"><span data-stu-id="680ff-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="680ff-199">grupo de Hola "*temporal*" puede contener uno o varios roles de una o varias de las aplicaciones implementadas en su cuenta de plataforma en la nube SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="680ff-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="680ff-200">Utilice grupos basados en aserción cuando desee asignar toosimultaneously tooone muchos de los usuarios o más roles de las aplicaciones en su cuenta de plataforma en la nube SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="680ff-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="680ff-201">Si desea que solo un número único o pequeño de usuarios toospecific funciones tooassign, recomendamos asignarlos directamente en hello "**autorizaciones**" pestaña de cabina de plataforma en la nube SAP HANA Hola.</span><span class="sxs-lookup"><span data-stu-id="680ff-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="680ff-202">Asignar a un usuario de tooa de rol</span><span class="sxs-lookup"><span data-stu-id="680ff-202">Assign a role tooa user</span></span>
<span data-ttu-id="680ff-203">En orden tooenable toolog de los usuarios de Azure AD en plataforma en la nube SAP HANA, debe asignar roles de hello toothem de plataforma en la nube SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="680ff-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="680ff-204">**tooassign un usuario de tooa rol, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="680ff-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="680ff-205">Inicie sesión en tooyour **plataforma en la nube SAP HANA** cabina.</span><span class="sxs-lookup"><span data-stu-id="680ff-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="680ff-206">Realice Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="680ff-206">Perform hello following:</span></span>
   
   <span data-ttu-id="680ff-207">![Autorizaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizaciones")</span><span class="sxs-lookup"><span data-stu-id="680ff-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="680ff-208">Haga clic en **Authorization**(Autorización).</span><span class="sxs-lookup"><span data-stu-id="680ff-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="680ff-209">Haga clic en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="680ff-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="680ff-210">Hola **usuario** cuadro de texto, dirección de correo electrónico del usuario de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="680ff-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="680ff-211">Haga clic en **asignar** rol tooa de tooassign Hola usuario.</span><span class="sxs-lookup"><span data-stu-id="680ff-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="680ff-212">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="680ff-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="680ff-213">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="680ff-213">Assign users</span></span>
<span data-ttu-id="680ff-214">tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.</span><span class="sxs-lookup"><span data-stu-id="680ff-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="680ff-215">**tooassign usuarios tooSAP plataforma de nube de HANA, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="680ff-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="680ff-216">Hola portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="680ff-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="680ff-217">En hello **plataforma en la nube SAP HANA** página de integración de aplicaciones, haga clic en **asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="680ff-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="680ff-218">![Asignar usuarios](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="680ff-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="680ff-219">Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.</span><span class="sxs-lookup"><span data-stu-id="680ff-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="680ff-220">![Sí](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="680ff-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="680ff-221">Si desea tootest la configuración de SSO, abra Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="680ff-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="680ff-222">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="680ff-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

