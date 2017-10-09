---
title: "aaaAzure AD Android Introducción | Documentos de Microsoft"
description: "¿Cómo toobuild una aplicación Android que se integra con Azure AD para inicio de sesión y llamadas a Azure AD había protegido API mediante OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="61a77-103">Integración de Azure AD en una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="61a77-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="61a77-104">Probar la versión preliminar de Hola de nuestra nueva [portal para desarrolladores de](https://identity.microsoft.com/Docs/Android), que le ayudará a ponerse a trabajar con Azure AD en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="61a77-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="61a77-105">portal para desarrolladores de Hello le guiará a través del proceso de Hola de registrar una aplicación y la integración de Azure AD en el código.</span><span class="sxs-lookup"><span data-stu-id="61a77-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="61a77-106">Cuando haya terminado, tendrá una aplicación sencilla que podrá autenticar a los usuarios del inquilino, así como un back-end con capacidad para aceptar tokens y realizar validaciones.</span><span class="sxs-lookup"><span data-stu-id="61a77-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="61a77-107">Si está desarrollando una aplicación de escritorio, Azure Active Directory (Azure AD) hace simple y sencillo para tooauthenticate los usuarios mediante sus cuentas de Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="61a77-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="61a77-108">También permite que su aplicación toosecurely consumir cualquier web API protegida por Azure AD, como Hola API de Office 365 u Hola API de Azure.</span><span class="sxs-lookup"><span data-stu-id="61a77-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="61a77-109">Para los clientes de Android que necesitan recursos tooaccess protegido, Azure AD proporciona Hola biblioteca de autenticación de Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="61a77-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="61a77-110">Hola único propósito de AAL es toomake más sencilla para los tokens de acceso de tooget de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="61a77-111">toodemonstrate lo fácil es, vamos a crear una aplicación Android lista de tareas que:</span><span class="sxs-lookup"><span data-stu-id="61a77-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="61a77-112">Obtiene acceso a los tokens para llamar a una API de la lista de tareas mediante el uso de hello [protocolo de autenticación de OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="61a77-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="61a77-113">Obtener listas de tareas pendientes de un usuario.</span><span class="sxs-lookup"><span data-stu-id="61a77-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="61a77-114">Desconectar a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="61a77-114">Signs out users.</span></span>

<span data-ttu-id="61a77-115">tooget iniciado, necesita a un inquilino de Azure AD en el que puede crear usuarios y registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="61a77-116">Si aún no tiene un inquilino, [Obtenga información acerca de cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="61a77-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="61a77-117">Paso 1: Descargue y ejecute el servidor de ejemplo de Hola tareas de API de REST de Node.js</span><span class="sxs-lookup"><span data-stu-id="61a77-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="61a77-118">ejemplo de Hola a tareas de API de REST de Node.js se escribe específicamente toowork en nuestro ejemplo existente para la creación de un API de REST de tareas pendientes de único inquilino para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61a77-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="61a77-119">Se trata de un requisito previo para hello inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="61a77-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="61a77-120">Para obtener información sobre cómo tooset este proceso, consulte nuestros ejemplos existentes en [Microsoft Azure Active Directory REST API de servicio de ejemplo para Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="61a77-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="61a77-121">Paso 2: registre la API web con el inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="61a77-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="61a77-122">Active Directory permite agregar dos tipos de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="61a77-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="61a77-123">Las API que ofrecen servicios toousers Web</span><span class="sxs-lookup"><span data-stu-id="61a77-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="61a77-124">Aplicaciones (se ejecutan en web de Hola o en un dispositivo) que tienen acceso a los que las API web</span><span class="sxs-lookup"><span data-stu-id="61a77-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="61a77-125">En este paso, que se está registrando hello web API que se ejecutan localmente para probar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="61a77-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="61a77-126">Normalmente, esta API web es un servicio REST que es una funcionalidad de oferta que desea que un tooaccess de aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="61a77-127">Azure AD puede ayudar a proteger cualquier punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="61a77-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="61a77-128">Suponemos que está registrando Hola API de REST de tareas hace referencia a versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="61a77-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="61a77-129">Pero esto funciona para cualquier API web en la que desea proteger toohelp de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="61a77-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="61a77-130">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61a77-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61a77-131">En la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="61a77-131">On hello top bar, click your account.</span></span> <span data-ttu-id="61a77-132">Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="61a77-133">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61a77-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="61a77-134">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="61a77-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="61a77-135">Escriba un nombre descriptivo para la aplicación hello (por ejemplo, **TodoListService**), seleccione **aplicación Web o API Web**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="61a77-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="61a77-136">Hola inicio de sesión en la dirección URL, escriba URL base Hola de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="61a77-137">De manera predeterminada, será `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="61a77-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="61a77-138">Haga clic en **Aceptar** registro de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="61a77-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="61a77-139">Mientras se encuentra en hello portal de Azure, ir a página de aplicación tooyour, buscar el valor de identificador de aplicación hello y cópiela.</span><span class="sxs-lookup"><span data-stu-id="61a77-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="61a77-140">Lo necesitará más adelante cuando configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="61a77-141">De hello **configuración** -> **propiedades** página, actualizar la aplicación hello URI del Id.: Introduzca `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="61a77-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="61a77-142">Reemplace `<your_tenant_name>` por nombre de hello del inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61a77-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="61a77-143">Paso 3: Registrar aplicación de Android Native Client de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="61a77-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="61a77-144">Debe registrar la aplicación web en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="61a77-144">You must register your web application in this sample.</span></span> <span data-ttu-id="61a77-145">Esto permite que su toocommunicate de aplicación con API web recién registrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="61a77-146">Azure AD rechazará tooeven permitir su tooask de aplicación para inicio de sesión a menos que se registra.</span><span class="sxs-lookup"><span data-stu-id="61a77-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="61a77-147">Que forma parte de la seguridad de hello del modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="61a77-148">Suponemos que está registrando la aplicación de ejemplo de Hola mencionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="61a77-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="61a77-149">No obstante, este procedimiento sirve para cualquier aplicación que esté desarrollando.</span><span class="sxs-lookup"><span data-stu-id="61a77-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="61a77-150">Es posible que se pregunte por qué poner una aplicación y una API web en un mismo inquilino.</span><span class="sxs-lookup"><span data-stu-id="61a77-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="61a77-151">Como posiblemente haya intuido, puede crear una aplicación con acceso a una API externa registrada en Azure AD desde otro inquilino.</span><span class="sxs-lookup"><span data-stu-id="61a77-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="61a77-152">Si lo hace, sus clientes podrán solicita tooconsent toohello uso de hello API en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="61a77-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="61a77-153">La Biblioteca de autenticación de Active Directory para iOS se encarga de este consentimiento por usted.</span><span class="sxs-lookup"><span data-stu-id="61a77-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="61a77-154">A medida que exploramos características más avanzadas, verá que se trata de una parte importante del conjunto de hello trabajo tooaccess necesarios Hola de APIs de Microsoft de Azure y Office, así como cualquier otro proveedor de servicio.</span><span class="sxs-lookup"><span data-stu-id="61a77-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="61a77-155">Por ahora, ya ha registrado su API web y la aplicación sometida a Hola mismo inquilino, no verá las peticiones de consentimiento.</span><span class="sxs-lookup"><span data-stu-id="61a77-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="61a77-156">Esto suele ser el caso de hello si está desarrollando una aplicación solo para su propio toouse de empresa.</span><span class="sxs-lookup"><span data-stu-id="61a77-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="61a77-157">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61a77-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61a77-158">En la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="61a77-158">On hello top bar, click your account.</span></span> <span data-ttu-id="61a77-159">Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="61a77-160">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="61a77-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="61a77-161">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="61a77-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="61a77-162">Escriba un nombre descriptivo para la aplicación hello (por ejemplo, **TodoListClient Android**), seleccione **aplicación cliente nativa**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="61a77-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="61a77-163">URI de redireccionamiento para hello, escriba `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="61a77-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="61a77-164">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="61a77-164">Click **Finish**.</span></span>
7. <span data-ttu-id="61a77-165">Página de aplicación Hola, buscar el valor de identificador de aplicación hello y cópiela.</span><span class="sxs-lookup"><span data-stu-id="61a77-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="61a77-166">Lo necesitará más adelante cuando configure la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="61a77-167">De hello **configuración** página, seleccione **permisos necesarios** y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="61a77-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="61a77-168">Busque y seleccione TodoListService, agregue hello **acceso TodoListService** permiso en **permisos delegados**y haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="61a77-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="61a77-169">toobuild con Maven, puede usar pom.xml en el nivel superior de hello:</span><span class="sxs-lookup"><span data-stu-id="61a77-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="61a77-170">Clone este repositorio en el directorio que desee:</span><span class="sxs-lookup"><span data-stu-id="61a77-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="61a77-171">Siga los pasos de Hola Hola [tooset de requisitos previos del entorno de Maven para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="61a77-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="61a77-172">Configurar el emulador de hello con SDK 19.</span><span class="sxs-lookup"><span data-stu-id="61a77-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="61a77-173">Vaya a carpeta de raíz de toohello donde clonó repositorio Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="61a77-174">Ejecute este comando: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="61a77-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="61a77-175">Cambiar directorio toohello inicio rápido muestra de Hola a:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="61a77-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="61a77-176">Ejecute este comando: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="61a77-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="61a77-177">Debería ver la aplicación a partir de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="61a77-178">Escriba tootry de credenciales de usuario de prueba.</span><span class="sxs-lookup"><span data-stu-id="61a77-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="61a77-179">Se van a enviar paquetes JAR junto a paquetes de saludo AAR.</span><span class="sxs-lookup"><span data-stu-id="61a77-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="61a77-180">Paso 4: Descargar Hola Android AAL y agregar área de trabajo de Eclipse tooyour</span><span class="sxs-lookup"><span data-stu-id="61a77-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="61a77-181">Que hemos hecho fácil para toohave varias opciones toouse ADAL en el proyecto de Android:</span><span class="sxs-lookup"><span data-stu-id="61a77-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="61a77-182">Puede usar esta biblioteca de tooimport de código de origen de hello en Eclipse y vínculo tooyour una aplicación.</span><span class="sxs-lookup"><span data-stu-id="61a77-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="61a77-183">Si usa Android Studio, puede usar Hola AAR paquete formato y referencia Hola archivos binarios.</span><span class="sxs-lookup"><span data-stu-id="61a77-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="61a77-184">Opción 1: origen a través de ZIP</span><span class="sxs-lookup"><span data-stu-id="61a77-184">Option 1: Source Zip</span></span>
<span data-ttu-id="61a77-185">toodownload una copia del código fuente de hello, haga clic en **Download ZIP** en hello derecha de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="61a77-186">También puede [descargarla desde GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="61a77-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="61a77-187">Opción 2: origen a través de Git</span><span class="sxs-lookup"><span data-stu-id="61a77-187">Option 2: Source via Git</span></span>
<span data-ttu-id="61a77-188">código de origen de hello tooget de hello SDK mediante Git, escriba:</span><span class="sxs-lookup"><span data-stu-id="61a77-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="61a77-189">Opción 3: binarios a través de Gradle</span><span class="sxs-lookup"><span data-stu-id="61a77-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="61a77-190">Puede obtener los archivos binarios de Hola de repositorio central de hello Maven.</span><span class="sxs-lookup"><span data-stu-id="61a77-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="61a77-191">paquete de AAR Hola se puede incluir los siguientes en el proyecto en Android Studio:</span><span class="sxs-lookup"><span data-stu-id="61a77-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="61a77-192">Opción 4: AAR a través de Maven</span><span class="sxs-lookup"><span data-stu-id="61a77-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="61a77-193">Si usas hello M2Eclipse complemento, puede especificar dependencias de hello en el archivo pom.xml:</span><span class="sxs-lookup"><span data-stu-id="61a77-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="61a77-194">Opción 5: Paquete JAR dentro de la carpeta de bibliotecas de Hola</span><span class="sxs-lookup"><span data-stu-id="61a77-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="61a77-195">Puede obtener archivo JAR de hello de repositorio de Maven hello y colóquelo en hello **bibliotecas** carpeta del proyecto.</span><span class="sxs-lookup"><span data-stu-id="61a77-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="61a77-196">Necesita toocopy Hola requiere recursos tooyour project, porque no incluyen paquetes de saludo JAR.</span><span class="sxs-lookup"><span data-stu-id="61a77-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="61a77-197">Paso 5: Agregar proyecto de referencias tooAndroid tooyour ADAL</span><span class="sxs-lookup"><span data-stu-id="61a77-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="61a77-198">Agregue una referencia de proyecto de tooyour y especificarla como una biblioteca de Android.</span><span class="sxs-lookup"><span data-stu-id="61a77-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="61a77-199">Si no está seguro cómo toodo esto, puede obtener más información sobre hello [sitio Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="61a77-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="61a77-200">Agregar dependencia de proyecto de hello para la depuración en la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="61a77-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="61a77-201">Actualizar tooinclude de archivo AndroidManifest.xml del proyecto:</span><span class="sxs-lookup"><span data-stu-id="61a77-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="61a77-202">Cree una instancia de AuthenticationContext en la actividad principal.</span><span class="sxs-lookup"><span data-stu-id="61a77-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="61a77-203">detalles de Hola de esta llamada son más allá del ámbito de Hola de este tema, pero puede empezar a trabajar examinando hello [ejemplo de Android Native Client](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="61a77-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="61a77-204">En el siguiente ejemplo de Hola, SharedPreferences es la memoria caché predeterminada de Hola y entidad está en forma de Hola de `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="61a77-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="61a77-205">Copie este extremo de Hola de toohandle de bloque de código de AuthenticationActivity después de usuario de hello escribe las credenciales y recibe un código de autorización:</span><span class="sxs-lookup"><span data-stu-id="61a77-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="61a77-206">tooask para un token, defina una devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="61a77-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="61a77-207">Por último, solicite un token mediante esa devolución de llamada:</span><span class="sxs-lookup"><span data-stu-id="61a77-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="61a77-208">Aquí se muestra una explicación de los parámetros de hello:</span><span class="sxs-lookup"><span data-stu-id="61a77-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="61a77-209">*recursos* es necesaria y recursos de Hola que está tratando de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="61a77-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="61a77-210">*clientid* es necesario. Su valor procede de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61a77-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="61a77-211">*RedirectUri* no es necesario toobe proporcionada para la llamada de acquireToken Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="61a77-212">Se puede configurar como el nombre del paquete.</span><span class="sxs-lookup"><span data-stu-id="61a77-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="61a77-213">*PromptBehavior* le ayuda a tooask para caché de credenciales tooskip hello y cookies.</span><span class="sxs-lookup"><span data-stu-id="61a77-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="61a77-214">*devolución de llamada* se llama después de código de autorización de Hola se intercambia para un token.</span><span class="sxs-lookup"><span data-stu-id="61a77-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="61a77-215">La devolución de llamada tiene un objeto de AuthenticationResult que tiene acceso al token, fecha de caducidad e información sobre el token del identificador.</span><span class="sxs-lookup"><span data-stu-id="61a77-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="61a77-216">*acquireTokenSilent* es opcional.</span><span class="sxs-lookup"><span data-stu-id="61a77-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="61a77-217">Puede llamarlo toohandle almacenamiento en caché y la actualización del token.</span><span class="sxs-lookup"><span data-stu-id="61a77-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="61a77-218">También proporciona la versión de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-218">It also provides hello sync version.</span></span> <span data-ttu-id="61a77-219">Acepta *userId* como parámetro.</span><span class="sxs-lookup"><span data-stu-id="61a77-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="61a77-220">Mediante el uso de este tutorial, debe tener lo que necesita toosuccessfully integrar con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="61a77-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="61a77-221">Para obtener más ejemplos de este trabajo, visite hello AzureADSamples / repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="61a77-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="61a77-222">Información importante</span><span class="sxs-lookup"><span data-stu-id="61a77-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="61a77-223">Personalización</span><span class="sxs-lookup"><span data-stu-id="61a77-223">Customization</span></span>
<span data-ttu-id="61a77-224">Los recursos de la aplicación pueden sobrescribir a los recursos del proyecto de la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="61a77-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="61a77-225">Esto sucede cuando la aplicación se está generando.</span><span class="sxs-lookup"><span data-stu-id="61a77-225">This happens when your app is being built.</span></span> <span data-ttu-id="61a77-226">Por este motivo, puede personalizar la autenticación actividad diseño Hola que quieras.</span><span class="sxs-lookup"><span data-stu-id="61a77-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="61a77-227">Ser seguro tookeep Hola ID de controles de Hola que AAL usa (WebView).</span><span class="sxs-lookup"><span data-stu-id="61a77-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="61a77-228">Agente</span><span class="sxs-lookup"><span data-stu-id="61a77-228">Broker</span></span>
<span data-ttu-id="61a77-229">aplicación de Portal de empresa de Microsoft Intune Hello proporciona componentes de broker de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="61a77-230">se crea la cuenta de Hello en el Administrador de cuentas.</span><span class="sxs-lookup"><span data-stu-id="61a77-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="61a77-231">tipo de cuenta de Hello es "com.microsoft.workaccount."</span><span class="sxs-lookup"><span data-stu-id="61a77-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="61a77-232">El administrador de cuentas únicamente permite una sola cuenta SSO.</span><span class="sxs-lookup"><span data-stu-id="61a77-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="61a77-233">Crea una cookie SSO para el usuario Hola después de completar el desafío de dispositivo de Hola para una de las aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="61a77-234">AAL usa la cuenta del agente de Hola si se crea una cuenta de usuario en este autenticador y elige no tooskip lo.</span><span class="sxs-lookup"><span data-stu-id="61a77-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="61a77-235">Puede omitir el usuario de broker de hello con:</span><span class="sxs-lookup"><span data-stu-id="61a77-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="61a77-236">Deberá tooregister un RedirectUri especial para el uso de broker.</span><span class="sxs-lookup"><span data-stu-id="61a77-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="61a77-237">RedirectUri está en formato de Hola de `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="61a77-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="61a77-238">Puede obtener su RedirectUri de la aplicación mediante brokerRedirectPrint.ps1 de script de Hola u Hola API llamada mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="61a77-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="61a77-239">firma de Hello es relacionado tooyour certificados de firma.</span><span class="sxs-lookup"><span data-stu-id="61a77-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="61a77-240">modelo de broker actual Hello es para un usuario.</span><span class="sxs-lookup"><span data-stu-id="61a77-240">hello current broker model is for one user.</span></span> <span data-ttu-id="61a77-241">AuthenticationContext proporciona el usuario de broker de hello API método tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="61a77-242">El manifiesto de aplicación debe tener Hola siguiendo las cuentas de administrador de cuentas de toouse de permisos.</span><span class="sxs-lookup"><span data-stu-id="61a77-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="61a77-243">Para obtener más información, vea hello [información del Administrador de cuentas en el sitio de Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="61a77-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="61a77-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="61a77-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="61a77-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="61a77-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="61a77-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="61a77-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="61a77-247">AD FS y URL de la autoridad</span><span class="sxs-lookup"><span data-stu-id="61a77-247">Authority URL and AD FS</span></span>
<span data-ttu-id="61a77-248">Los servicios de federación de Active Directory (AD FS) no se reconoce como producción STS, por lo que necesita tooturn de detección de instancia y pase el valor false en el constructor de AuthenticationContext Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="61a77-249">dirección URL de la entidad emisora de Hello necesita una instancia de STS y un [nombre del inquilino](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="61a77-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="61a77-250">Consulta de los elementos en caché</span><span class="sxs-lookup"><span data-stu-id="61a77-250">Querying cache items</span></span>
<span data-ttu-id="61a77-251">ADAL proporciona memoria caché predeterminada en SharedPreferences con algunas características sencillas para hacer consultas sobre los elementos en caché.</span><span class="sxs-lookup"><span data-stu-id="61a77-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="61a77-252">Puede obtener de caché actual Hola de AuthenticationContext mediante:</span><span class="sxs-lookup"><span data-stu-id="61a77-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="61a77-253">También puede proporcionar la implementación de la memoria caché, si desea que toocustomize lo.</span><span class="sxs-lookup"><span data-stu-id="61a77-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="61a77-254">Comportamiento de la petición</span><span class="sxs-lookup"><span data-stu-id="61a77-254">Prompt behavior</span></span>
<span data-ttu-id="61a77-255">AAL proporciona un comportamiento de solicitud de toospecify de opción.</span><span class="sxs-lookup"><span data-stu-id="61a77-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="61a77-256">PromptBehavior.Auto mostrará Hola interfaz de usuario si no es válido el token de actualización de Hola y se necesitan credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="61a77-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="61a77-257">PromptBehavior.Always se omita el uso de la memoria caché de Hola y mostrar siempre Hola interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="61a77-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="61a77-258">Solicitud de token silenciosa desde la memoria caché y actualización</span><span class="sxs-lookup"><span data-stu-id="61a77-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="61a77-259">Una solicitud de token silenciosa no utiliza Hola emergente de la interfaz de usuario y no requiere una actividad.</span><span class="sxs-lookup"><span data-stu-id="61a77-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="61a77-260">Devuelve un token de caché de hello si está disponible.</span><span class="sxs-lookup"><span data-stu-id="61a77-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="61a77-261">Si expira el token de hello, este método intenta toorefresh lo.</span><span class="sxs-lookup"><span data-stu-id="61a77-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="61a77-262">Si el token de actualización de hello está caducado o no correctamente, devuelve AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="61a77-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="61a77-263">También puede hacer una llamada de sincronización con este método.</span><span class="sxs-lookup"><span data-stu-id="61a77-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="61a77-264">Puede establecer toocallback null o usar acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="61a77-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="61a77-265">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="61a77-265">Diagnostics</span></span>
<span data-ttu-id="61a77-266">Estas son las principales fuentes de Hola de información para diagnosticar problemas:</span><span class="sxs-lookup"><span data-stu-id="61a77-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="61a77-267">Excepciones</span><span class="sxs-lookup"><span data-stu-id="61a77-267">Exceptions</span></span>
* <span data-ttu-id="61a77-268">Registros</span><span class="sxs-lookup"><span data-stu-id="61a77-268">Logs</span></span>
* <span data-ttu-id="61a77-269">Seguimientos de red</span><span class="sxs-lookup"><span data-stu-id="61a77-269">Network traces</span></span>

<span data-ttu-id="61a77-270">Tenga en cuenta que los identificadores de correlación son diagnósticos toohello central en la biblioteca de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="61a77-271">Puede establecer los identificadores de correlación en cada solicitud si desea toocorrelate una ADAL solicitar con otras operaciones en el código.</span><span class="sxs-lookup"><span data-stu-id="61a77-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="61a77-272">Si no establece un identificador de correlación, ADAL generará uno aleatorio.</span><span class="sxs-lookup"><span data-stu-id="61a77-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="61a77-273">Todos los mensajes de registro y llamadas de red, a continuación, se mostrarán con el identificador de correlación de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="61a77-274">Hola autogenerado Id. los cambios en cada solicitud.</span><span class="sxs-lookup"><span data-stu-id="61a77-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="61a77-275">Excepciones</span><span class="sxs-lookup"><span data-stu-id="61a77-275">Exceptions</span></span>
<span data-ttu-id="61a77-276">Las excepciones son Hola primero diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="61a77-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="61a77-277">Intentamos tooprovide mensajes de error útiles.</span><span class="sxs-lookup"><span data-stu-id="61a77-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="61a77-278">Si encuentra alguno que no sea útil, genere un caso y háganoslo saber.</span><span class="sxs-lookup"><span data-stu-id="61a77-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="61a77-279">Proporcione también información sobre el dispositivo, por ejemplo, el modelo y el número de SDK.</span><span class="sxs-lookup"><span data-stu-id="61a77-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="61a77-280">Registros</span><span class="sxs-lookup"><span data-stu-id="61a77-280">Logs</span></span>
<span data-ttu-id="61a77-281">Puede configurar Hola biblioteca toogenerate mensajes de registro que se puede usar toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="61a77-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="61a77-282">Configurar el registro realizar Hola siguiente llamada a tooconfigure que AAL utilizará toohand desactivar cada mensaje del registro cuando se genera una devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="61a77-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="61a77-283">Se pueden escribir mensajes tooa archivo de registro personalizado, como se muestra en el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="61a77-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="61a77-284">Por desgracia, no hay ninguna manera estándar de obtener los registros de un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="61a77-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="61a77-285">Hay algunos servicios que pueden ayudar con esta tarea.</span><span class="sxs-lookup"><span data-stu-id="61a77-285">There are some services that can help you with this.</span></span> <span data-ttu-id="61a77-286">También puede inventar su propio, como servidor de tooa de archivo hello envío.</span><span class="sxs-lookup"><span data-stu-id="61a77-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="61a77-287">Estos son los niveles de registro de hello:</span><span class="sxs-lookup"><span data-stu-id="61a77-287">These are hello logging levels:</span></span>
* <span data-ttu-id="61a77-288">Error (excepciones)</span><span class="sxs-lookup"><span data-stu-id="61a77-288">Error (exceptions)</span></span>
* <span data-ttu-id="61a77-289">Warn (advertencia)</span><span class="sxs-lookup"><span data-stu-id="61a77-289">Warn (warning)</span></span>
* <span data-ttu-id="61a77-290">Info (información)</span><span class="sxs-lookup"><span data-stu-id="61a77-290">Info (information purposes)</span></span>
* <span data-ttu-id="61a77-291">Verbose (más detalles)</span><span class="sxs-lookup"><span data-stu-id="61a77-291">Verbose (more details)</span></span>

<span data-ttu-id="61a77-292">Establecer el nivel de registro de hello similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="61a77-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="61a77-293">Todos los mensajes de registro se envían toologcat, en las devoluciones de llamada de adición tooany registro personalizado.</span><span class="sxs-lookup"><span data-stu-id="61a77-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="61a77-294">Puede obtener un archivo de registro de tooa desde logcat como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="61a77-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="61a77-295">Para obtener más información acerca de los comandos de adb, vea hello [logcat información en el sitio de Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="61a77-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="61a77-296">Seguimientos de red</span><span class="sxs-lookup"><span data-stu-id="61a77-296">Network traces</span></span>
<span data-ttu-id="61a77-297">Puede utilizar diversas herramientas toocapture Hola tráfico HTTP que genera AAL.</span><span class="sxs-lookup"><span data-stu-id="61a77-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="61a77-298">Esto es muy útil si está familiarizado con el protocolo OAuth Hola o si necesita tooprovide información de diagnóstico tooMicrosoft u otros canales de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="61a77-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="61a77-299">Fiddler es la herramienta de seguimiento de HTTP más sencilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="61a77-300">Siguientes de Hola de uso vínculos tooset, configúrelo toocorrectly registro AAL tráfico de red.</span><span class="sxs-lookup"><span data-stu-id="61a77-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="61a77-301">Para obtener una herramienta de seguimiento como Fiddler o Charles toobe útil, debe configurarlo toorecord sin cifrar el tráfico SSL.</span><span class="sxs-lookup"><span data-stu-id="61a77-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="61a77-302">Los seguimientos generados de esta manera pueden contener información altamente privilegiada, como tokens de acceso, nombres de usuario y contraseñas.</span><span class="sxs-lookup"><span data-stu-id="61a77-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="61a77-303">Si utiliza cuentas de producción, no comparta esta información con terceras partes.</span><span class="sxs-lookup"><span data-stu-id="61a77-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="61a77-304">Si necesita toosupply un toosomeone de seguimiento en la compatibilidad de orden tooget, reproduzca el problema de hello mediante una cuenta temporal con nombres de usuario y contraseñas que no le importa de uso compartido.</span><span class="sxs-lookup"><span data-stu-id="61a77-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="61a77-305">Desde el sitio Web de Telerik hello: [configuración de seguridad de Fiddler para Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="61a77-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="61a77-306">En GitHub, consulte cómo [configurar reglas de Fiddler para ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler).</span><span class="sxs-lookup"><span data-stu-id="61a77-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="61a77-307">Modo de diálogo</span><span class="sxs-lookup"><span data-stu-id="61a77-307">Dialog mode</span></span>
<span data-ttu-id="61a77-308">método de acquireToken de Hello sin actividad es compatible con un símbolo del sistema del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="61a77-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="61a77-309">Cifrado</span><span class="sxs-lookup"><span data-stu-id="61a77-309">Encryption</span></span>
<span data-ttu-id="61a77-310">AAL cifra los tokens de Hola y almacén en SharedPreferences de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="61a77-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="61a77-311">Puede buscar en los detalles de Hola Hola StorageHelper clase toosee.</span><span class="sxs-lookup"><span data-stu-id="61a77-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="61a77-312">Android introdujo el almacenamiento seguro de claves privadas AndroidKeyStore 4.3 (API18).</span><span class="sxs-lookup"><span data-stu-id="61a77-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="61a77-313">ADAL lo utiliza para API 18 y las versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="61a77-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="61a77-314">Si desea toouse AAL para las versiones inferiores de SDK, deberá tooprovide una clave secreta en AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="61a77-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="61a77-315">Desafío de portador de Oauth2</span><span class="sxs-lookup"><span data-stu-id="61a77-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="61a77-316">Hola AuthenticationParameters clase proporciona funcionalidad tooget authorization_uri de hello desafío de portador de OAuth2.</span><span class="sxs-lookup"><span data-stu-id="61a77-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="61a77-317">Cookies de sesión en WebView</span><span class="sxs-lookup"><span data-stu-id="61a77-317">Session cookies in WebView</span></span>
<span data-ttu-id="61a77-318">Android WebView no borra las cookies de sesión después de cerrar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="61a77-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="61a77-319">Esto puede controlarse mediante el siguiente código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="61a77-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="61a77-320">Para obtener más información acerca de las cookies, consulte hello [CookieSyncManager información en el sitio de Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="61a77-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="61a77-321">Reemplazos de recursos</span><span class="sxs-lookup"><span data-stu-id="61a77-321">Resource overrides</span></span>
<span data-ttu-id="61a77-322">biblioteca ADAL de Hello incluye cadenas en inglés para los mensajes de ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="61a77-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="61a77-323">La aplicación debe sobrescribirlas si desea ver las cadenas traducidas.</span><span class="sxs-lookup"><span data-stu-id="61a77-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="61a77-324">Cuadro de diálogo NTLM</span><span class="sxs-lookup"><span data-stu-id="61a77-324">NTLM dialog box</span></span>
<span data-ttu-id="61a77-325">AAL versión 1.1.0 admite un cuadro de diálogo NTLM que se procesa a través de eventos de hello onReceivedHttpAuthRequest desde WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="61a77-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="61a77-326">Puede personalizar el diseño de Hola y cadenas para el cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="61a77-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="61a77-327">SSO entre aplicaciones</span><span class="sxs-lookup"><span data-stu-id="61a77-327">Cross-app SSO</span></span>
<span data-ttu-id="61a77-328">Obtenga información acerca de [cómo tooenable SSO de aplicación cruzado en Android mediante el uso de ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="61a77-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
