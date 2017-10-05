---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform | Microsoft Docs"
description: "Aprenda cómo usar SAP HANA Cloud Platform con Azure Active Directory para habilitar el inicio de sesión único, el aprovisionamiento automatizado, etc."
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
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="023bd-103">Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="023bd-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="023bd-104">El objetivo de este tutorial es mostrar la integración de Azure y SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="023bd-105">En la situación descrita en este tutorial se supone que ya cuenta con los elementos siguientes:</span><span class="sxs-lookup"><span data-stu-id="023bd-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="023bd-106">Una suscripción de Azure válida</span><span class="sxs-lookup"><span data-stu-id="023bd-106">A valid Azure subscription</span></span>
* <span data-ttu-id="023bd-107">Una cuenta de SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="023bd-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="023bd-108">Después de completar este tutorial, los usuarios de Azure AD que ha asignado a SAP HANA Cloud Platform podrán realizar un inicio de sesión único en la aplicación con la [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="023bd-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="023bd-109">Deberá implementar su propia aplicación o suscribirse a una aplicación en su cuenta de SAP HANA Cloud Platform para probar el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="023bd-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="023bd-110">En este tutorial, se implementa una aplicación en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="023bd-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="023bd-111">La situación descrita en este tutorial consta de los siguientes bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="023bd-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="023bd-112">Habilitación de la integración de aplicaciones para SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="023bd-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="023bd-113">Configuración del inicio de sesión único (SSO)</span><span class="sxs-lookup"><span data-stu-id="023bd-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="023bd-114">Asignación de un rol a un usuario</span><span class="sxs-lookup"><span data-stu-id="023bd-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="023bd-115">Asignación de usuarios</span><span class="sxs-lookup"><span data-stu-id="023bd-115">Assigning users</span></span>

<span data-ttu-id="023bd-116">![Escenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Escenario")</span><span class="sxs-lookup"><span data-stu-id="023bd-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="023bd-117">Habilitación de la integración de aplicaciones para SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="023bd-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="023bd-118">El objetivo de esta sección es describir cómo habilitar la integración de las aplicaciones para SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="023bd-119">**Siga estos pasos con el fin de habilitar la integración de aplicaciones para SAP HANA Cloud Platform:**</span><span class="sxs-lookup"><span data-stu-id="023bd-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="023bd-120">En el panel de navegación izquierdo del Portal de administración de Azure, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="023bd-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="023bd-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="023bd-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="023bd-122">En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.</span><span class="sxs-lookup"><span data-stu-id="023bd-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="023bd-123">Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.</span><span class="sxs-lookup"><span data-stu-id="023bd-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="023bd-124">![Aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="023bd-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="023bd-125">Haga clic en **Agregar** en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="023bd-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="023bd-126">![Agregar aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Agregar aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="023bd-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="023bd-127">En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.</span><span class="sxs-lookup"><span data-stu-id="023bd-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="023bd-128">![Agregar una aplicación de la galería](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Agregar una aplicación de la galería")</span><span class="sxs-lookup"><span data-stu-id="023bd-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="023bd-129">En el **cuadro de búsqueda**, escriba **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="023bd-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="023bd-130">![Galería de aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galería de aplicaciones")</span><span class="sxs-lookup"><span data-stu-id="023bd-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="023bd-131">En el panel de resultados, seleccione **SAP HANA Cloud Platform** y haga clic en **Completar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="023bd-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="023bd-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="023bd-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="023bd-133">Configurar inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="023bd-133">Configure single sign-on</span></span>

<span data-ttu-id="023bd-134">El objetivo de esta sección es describir cómo se habilita la autenticación de los usuarios en SAP HANA Cloud Platform con su cuenta de Azure AD usando el protocolo SAML basado en la federación.</span><span class="sxs-lookup"><span data-stu-id="023bd-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="023bd-135">Como parte de este procedimiento, es necesario cargar un certificado codificado en base 64 en su inquilino de SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="023bd-136">Si no está familiarizado con este procedimiento, consulte [Conversión de un certificado binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="023bd-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="023bd-137">**Siga estos pasos para configurar el inicio de sesión único:**</span><span class="sxs-lookup"><span data-stu-id="023bd-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="023bd-138">En el Portal de Azure clásico, en la página de integración de aplicaciones de **SAP HANA Cloud Platform**, haga clic en **Configurar inicio de sesión único** para abrir el cuadro de diálogo **Configurar inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="023bd-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="023bd-139">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="023bd-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="023bd-140">En la página **¿Cómo desea que los usuarios inicien sesión en SAP HANA Cloud Platform?**, seleccione **Inicio de sesión único de Microsoft Azure AD** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="023bd-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="023bd-141">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="023bd-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="023bd-142">En otra ventana del explorador web, inicie sesión en SAP HANA Cloud Platform Cockpit en https://account.\<host horizontal\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="023bd-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="023bd-143">Haga clic en la pestaña **Trust** (Confianza).</span><span class="sxs-lookup"><span data-stu-id="023bd-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="023bd-144">![Confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Confianza")</span><span class="sxs-lookup"><span data-stu-id="023bd-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="023bd-145">En la sección de administración de confianza, lleve a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="023bd-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="023bd-146">![Obtención de metadatos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obtención de metadatos")</span><span class="sxs-lookup"><span data-stu-id="023bd-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="023bd-147">Haga clic en la pestaña **Local Service Provide** (Proveedor de servicios local).</span><span class="sxs-lookup"><span data-stu-id="023bd-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="023bd-148">Para descargar el archivo de metadatos de SAP HANA Cloud Platform, haga clic en **Get Metadata**(Obtener metadatos).</span><span class="sxs-lookup"><span data-stu-id="023bd-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="023bd-149">En el Portal de Azure clásico, en la página **Configurar dirección URL** de la aplicación, realice los pasos siguientes y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="023bd-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="023bd-150">![Configurar dirección URL de la aplicación](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurar dirección URL de la aplicación")</span><span class="sxs-lookup"><span data-stu-id="023bd-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="023bd-151">En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL utilizada por los usuarios para iniciar sesión en la aplicación **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="023bd-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="023bd-152">Se trata de la URL específica de la cuenta de un recurso protegido en su aplicación SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="023bd-153">La dirección URL se basa en el patrón siguiente: *https://\<nombreDeAplicación\>\<nombreDeCuenta\>.\<host horizontal\>.ondemand.com/\<ruta\_al\_recurso\_protegido\>* (p. ej.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*).</span><span class="sxs-lookup"><span data-stu-id="023bd-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="023bd-154">Se trata de la URL de la aplicación SAP HANA Cloud Platform que requiere que autentique el usuario.</span><span class="sxs-lookup"><span data-stu-id="023bd-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="023bd-155">Abra el archivo de metadatos de SAP HANA Cloud Platform descargado y luego busque la etiqueta **ns3:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="023bd-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="023bd-156">Copie el valor del atributo **Ubicación** y péguelo en el cuadro de texto **URL de respuesta de SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="023bd-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="023bd-157">En la página **Configurar inicio de sesión único en SAP HANA Cloud Platform**, para descargar los metadatos, haga clic en **Descargar metadatos** y guarde el archivo en el equipo.</span><span class="sxs-lookup"><span data-stu-id="023bd-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="023bd-158">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="023bd-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="023bd-159">En SAP HANA Cloud Platform Cockpit, en la sección **Local Service Provider** (Proveedor de servicios local), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="023bd-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="023bd-160">![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Administración de confianza")</span><span class="sxs-lookup"><span data-stu-id="023bd-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="023bd-161">Haga clic en **Editar**.</span><span class="sxs-lookup"><span data-stu-id="023bd-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="023bd-162">En **Configuration Type** (Tipo de configuración), seleccione **Custom** (Personalizado).</span><span class="sxs-lookup"><span data-stu-id="023bd-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="023bd-163">Como **Local Provider Name**(Nombre de proveedor local), deje el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="023bd-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="023bd-164">Para generar una **Signing Key** (Clave de firma) y un par de claves **Signing Certificate** (Certificado de firma), haga clic en **Generate Key Pair** (Generar par de claves).</span><span class="sxs-lookup"><span data-stu-id="023bd-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="023bd-165">En **Principal Propagation** (Propagación de entidad de seguridad), seleccione **Disabled** (Deshabilitada).</span><span class="sxs-lookup"><span data-stu-id="023bd-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="023bd-166">En **Force Authentication** (Forzar autenticación), seleccione **Disabled** (Deshabilitado).</span><span class="sxs-lookup"><span data-stu-id="023bd-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="023bd-167">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="023bd-167">Click **Save**.</span></span>

9. <span data-ttu-id="023bd-168">Haga clic en la pestaña **Trusted Identity Provider** (Proveedor de identidades de confianza) y en **Add Trusted Identity Provider** (Agregar proveedor de identidad de confianza).</span><span class="sxs-lookup"><span data-stu-id="023bd-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="023bd-169">![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Administración de confianza")</span><span class="sxs-lookup"><span data-stu-id="023bd-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="023bd-170">Para administrar la lista de proveedores de identidades de confianza, deberá haber elegido el tipo de configuración personalizada en la sección del proveedor de servicios local.</span><span class="sxs-lookup"><span data-stu-id="023bd-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="023bd-171">Para el tipo de configuración predeterminado, tendrá una confianza implícita y no editable para el servicio de id. de SAP.</span><span class="sxs-lookup"><span data-stu-id="023bd-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="023bd-172">Para Ninguno, no tiene ninguna configuración de confianza.</span><span class="sxs-lookup"><span data-stu-id="023bd-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="023bd-173">Haga clic en la pestaña **General** y en **Browse** (Examinar) para cargar el archivo de metadatos descargados.</span><span class="sxs-lookup"><span data-stu-id="023bd-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="023bd-174">![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Administración de confianza")</span><span class="sxs-lookup"><span data-stu-id="023bd-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="023bd-175">Después de cargar el archivo de metadatos, los valores de **Dirección URL de inicio de sesión único**, **Dirección URL de cierre de sesión único** y **Certificado de firma** se rellenan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="023bd-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="023bd-176">Haga clic en la pestaña **Attributes** (Atributos).</span><span class="sxs-lookup"><span data-stu-id="023bd-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="023bd-177">En la pestaña **Attributes** (Atributos), realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="023bd-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="023bd-178">![Atributos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Atributos")</span><span class="sxs-lookup"><span data-stu-id="023bd-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="023bd-179">Haga clic en **Add Assertion-Based Attribute**(Agregar atributo basado en la aserción) y agregue los siguientes atributos basados en aserción:</span><span class="sxs-lookup"><span data-stu-id="023bd-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="023bd-180">Atributo de aserción</span><span class="sxs-lookup"><span data-stu-id="023bd-180">Assertion Attribute</span></span> | <span data-ttu-id="023bd-181">Atributo de entidad de seguridad</span><span class="sxs-lookup"><span data-stu-id="023bd-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="023bd-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="023bd-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="023bd-183">firstname</span><span class="sxs-lookup"><span data-stu-id="023bd-183">firstname</span></span> |
    | <span data-ttu-id="023bd-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="023bd-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="023bd-185">Lastname</span><span class="sxs-lookup"><span data-stu-id="023bd-185">lastname</span></span> |
    | <span data-ttu-id="023bd-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="023bd-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="023bd-187">email</span><span class="sxs-lookup"><span data-stu-id="023bd-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="023bd-188">La configuración de los atributos depende de cómo se desarrollan las aplicaciones en HCP, es decir, qué atributos esperan en la respuesta de SAML y con qué nombre (atributo de la entidad de seguridad) tienen acceso a este atributo en el código.</span><span class="sxs-lookup"><span data-stu-id="023bd-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="023bd-189">El **atributo predeterminado** de la captura de pantalla solo es para fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="023bd-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="023bd-190">No es necesario para que el escenario funcione.</span><span class="sxs-lookup"><span data-stu-id="023bd-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="023bd-191">Los nombres y valores para el **Principal Attribute** (Atributo principal) que se muestran en la captura de pantalla dependen de cómo se desarrolle la aplicación.</span><span class="sxs-lookup"><span data-stu-id="023bd-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="023bd-192">Es posible que la aplicación requiera diferentes asignaciones.</span><span class="sxs-lookup"><span data-stu-id="023bd-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="023bd-193">En el Portal de Azure clásico, en la página de diálogo **Configurar inicio de sesión único en SAP HANA Cloud Platform**, seleccione la confirmación de configuración de inicio de sesión único y haga clic en **Completar**.</span><span class="sxs-lookup"><span data-stu-id="023bd-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="023bd-194">![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurar inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="023bd-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="023bd-195">Grupos basados en aserción</span><span class="sxs-lookup"><span data-stu-id="023bd-195">Assertion-based groups</span></span>
<span data-ttu-id="023bd-196">Como paso opcional, puede configurar grupos basados en aserciones para su proveedor de identidades de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="023bd-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="023bd-197">El uso de grupos en SAP HANA Cloud Platform le permite asignar dinámicamente uno o más usuarios a uno o más roles en sus aplicaciones de SAP HANA Cloud Platform, determinados por los valores de los atributos de la aserción de SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="023bd-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="023bd-198">Por ejemplo, si la aserción contiene el atributo "*contrato=temporal*", puede que desee que se agreguen todos los usuarios afectados al grupo "*TEMPORAL*".</span><span class="sxs-lookup"><span data-stu-id="023bd-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="023bd-199">El grupo "*TEMPORAL*" puede contener uno o varios roles de una o más de las aplicaciones implementadas en la cuenta de SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="023bd-200">Use grupos basados en aserciones si quiere asignar de manera simultánea muchos usuarios a uno o más roles de las aplicaciones en su cuenta de SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="023bd-201">Si quiere asignar un número único o pequeño de usuarios a roles específicos, recomendamos asignarlos directamente en la pestaña "**Autorizaciones**" de la cabina de SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="023bd-202">Asignar de un rol a un usuario</span><span class="sxs-lookup"><span data-stu-id="023bd-202">Assign a role to a user</span></span>
<span data-ttu-id="023bd-203">Para permitir que los usuarios de Azure AD inicien sesión en SAP HANA Cloud Platform, debe asignarles roles en SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="023bd-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="023bd-204">**Para asignar un rol a un usuario, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="023bd-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="023bd-205">Inicie sesión en su cabina de **SAP HANA Cloud Platform** .</span><span class="sxs-lookup"><span data-stu-id="023bd-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="023bd-206">Lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="023bd-206">Perform the following:</span></span>
   
   <span data-ttu-id="023bd-207">![Autorizaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizaciones")</span><span class="sxs-lookup"><span data-stu-id="023bd-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="023bd-208">Haga clic en **Authorization**(Autorización).</span><span class="sxs-lookup"><span data-stu-id="023bd-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="023bd-209">Haga clic en la pestaña **Usuarios** .</span><span class="sxs-lookup"><span data-stu-id="023bd-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="023bd-210">En el cuadro de texto **User** (Usuario), escriba la dirección de correo electrónico del usuario.</span><span class="sxs-lookup"><span data-stu-id="023bd-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="023bd-211">Haga clic en **Assign** (Asignar) para asignar el usuario a un rol.</span><span class="sxs-lookup"><span data-stu-id="023bd-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="023bd-212">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="023bd-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="023bd-213">Asignar usuarios</span><span class="sxs-lookup"><span data-stu-id="023bd-213">Assign users</span></span>
<span data-ttu-id="023bd-214">Para probar la configuración, debe conceder acceso a los usuarios de Azure AD a los que quiere permitir el uso de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="023bd-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="023bd-215">**Para asignar usuarios a SAP HANA Cloud Platform, lleve a cabo los siguientes pasos:**</span><span class="sxs-lookup"><span data-stu-id="023bd-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="023bd-216">En el Portal de Azure clásico, cree una cuenta de prueba.</span><span class="sxs-lookup"><span data-stu-id="023bd-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="023bd-217">En la página de integración de aplicaciones de **SAP HANA Cloud Platform**, haga clic en **Asignar usuarios**.</span><span class="sxs-lookup"><span data-stu-id="023bd-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="023bd-218">![Asignar usuarios](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Asignar usuarios")</span><span class="sxs-lookup"><span data-stu-id="023bd-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="023bd-219">Seleccione su usuario de prueba, haga clic en **Asignar** y en **Sí** para confirmar la asignación.</span><span class="sxs-lookup"><span data-stu-id="023bd-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="023bd-220">![Sí](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sí")</span><span class="sxs-lookup"><span data-stu-id="023bd-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="023bd-221">Si desea probar la configuración de inicio de sesión único (SSO), abra el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="023bd-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="023bd-222">Para obtener más información sobre el Panel de acceso, vea [Introducción al Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="023bd-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

