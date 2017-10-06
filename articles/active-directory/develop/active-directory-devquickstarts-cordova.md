---
title: "aaaAzure AD Cordova Introducción | Documentos de Microsoft"
description: "Cómo toobuild una aplicación de Cordova que se integra con Azure AD para inicio de sesión y llama a las API de protegido por AD Azure mediante el uso de OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="8c8bb-103">Integración de Azure AD con una aplicación Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="8c8bb-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="8c8bb-104">Puede usar las aplicaciones de Apache Cordova toodevelop HTML5 y JavaScript que se pueden ejecutar en dispositivos móviles como aplicaciones nativas completas.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="8c8bb-105">Con Azure Active Directory (Azure AD), puede agregar aplicaciones de Cordova de tooyour de las capacidades de autenticación de empresarial.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="8c8bb-106">Un complemento Cordova ajusta los SDK nativos de Azure AD en iOS, Android, la Tienda Windows y Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="8c8bb-107">Mediante el complemento, puede mejorar el inicio de sesión toosupport de aplicación con cuentas de Active Directory de Windows Server de los usuarios, obtener acceso tooOffice 365 y las API de Azure e incluso ayudar a proteger web personalizado propio de tooyour de llamadas API.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="8c8bb-108">En este tutorial, usaremos Hola Apache Cordova complemento para la biblioteca de autenticación de Active Directory (ADAL) tooimprove una aplicación sencilla mediante la adición de hello siguientes características:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="8c8bb-109">Con solo unas líneas de código, autenticar a un usuario y obtener un token.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="8c8bb-110">Usar ese tooquery de API Graph de hello tooinvoke símbolo (token) de ese directorio y mostrar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="8c8bb-111">Utilizar autenticación de toominimize de caché de tokens AAL Hola solicita usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="8c8bb-112">toomake esas mejoras, necesita:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="8c8bb-113">Registrar una aplicación con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="8c8bb-114">Agregue código tooyour aplicación toorequest tokens.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="8c8bb-115">Agregar código toouse Hola token para consultar Hola API Graph y mostrar los resultados.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="8c8bb-116">Crear proyecto de implementación de hello Cordova con todas las plataformas de hello desea tootarget, agregar complemento Cordova AAL hello y probar soluciones de hello en emuladores.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c8bb-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8c8bb-117">Prerequisites</span></span>
<span data-ttu-id="8c8bb-118">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="8c8bb-119">Un inquilino de Azure AD que disponga de una cuenta con derechos de desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="8c8bb-120">Un entorno de desarrollo que ha configurado toouse Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="8c8bb-121">Si tiene tanto ya configurado, tener acceso directamente toostep 1.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="8c8bb-122">Si no tiene un inquilino de Azure AD, use hello [obtener instrucciones sobre cómo tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="8c8bb-123">Si no dispone de Apache Cordova configurado en su equipo, instalar Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="8c8bb-124">Git</span><span class="sxs-lookup"><span data-stu-id="8c8bb-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="8c8bb-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="8c8bb-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="8c8bb-126">[Interfaz de línea de comandos Cordova](https://cordova.apache.org/) (se instala fácilmente mediante el administrador de paquetes NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="8c8bb-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="8c8bb-127">Hola anterior instalaciones debería funcionar en hello PC y en hello Mac.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="8c8bb-128">Cada plataforma de destino tiene diferentes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="8c8bb-129">toobuild y ejecutar una aplicación para Tabletas de Windows o Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="8c8bb-130">Instale [Visual Studio 2013 para Windows con la actualización 2 o posterior](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express u otra versión) o [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="8c8bb-131">toobuild y ejecutar una aplicación para iOS:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="8c8bb-132">Instale Xcode 6.x o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="8c8bb-133">Descargar de hello [sitio para desarrolladores de Apple](http://developer.apple.com/downloads) o hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="8c8bb-134">Instale [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="8c8bb-135">Puede usarlo toostart aplicaciones de iOS en el simulador de iOS desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="8c8bb-136">(Se puede instalar fácilmente a través de terminal hello: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="8c8bb-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="8c8bb-137">toobuild y ejecutar una aplicación para Android:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="8c8bb-138">Instale el [Kit de desarrollo de Java (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="8c8bb-139">Asegúrese de que `JAVA_HOME` (variable de entorno) se ha configurado correctamente según la ruta de acceso de la instalación de JDK toohello (por ejemplo, C:\Program Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="8c8bb-140">Instalar [SDK de Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) y agregue hello `<android-sdk-location>\tools` tooyour de ubicación (por ejemplo, C:\tools\Android\android-sdk\tools) `PATH` variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="8c8bb-141">Abra el Administrador de Android SDK (por ejemplo, a través de hello terminal: `android`) e instalar:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="8c8bb-142">*Android 5.0.1 (API 21)*</span><span class="sxs-lookup"><span data-stu-id="8c8bb-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="8c8bb-143">*Herramientas de compilación de SDK de Android*, versión 19.1.0 o posterior</span><span class="sxs-lookup"><span data-stu-id="8c8bb-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="8c8bb-144">*Repositorio compatible con Android* (extras)</span><span class="sxs-lookup"><span data-stu-id="8c8bb-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="8c8bb-145">Hola SDK de Android no proporciona ninguna instancia del emulador predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="8c8bb-146">Crear uno mediante la ejecución de `android avd` de hello terminal y, a continuación, seleccione **crear**, si desea que la aplicación de Android toorun hello en un emulador.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="8c8bb-147">Se recomienda un nivel de API de 19 o superior.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="8c8bb-148">Para obtener más información acerca de las opciones de creación y el emulador de Android hello, consulte [administrador AVD](http://developer.android.com/tools/help/avd-manager.html) en el sitio de hello Android.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="8c8bb-149">Paso 1: Registro de una aplicación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c8bb-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="8c8bb-150">Este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-150">This step is optional.</span></span> <span data-ttu-id="8c8bb-151">Este tutorial proporciona valores aprovisionados previamente que puede usar toosee Hola ejemplo en acción sin tener que realizar cualquier aprovisionamiento en su propio inquilino.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="8c8bb-152">Sin embargo, recomendamos que realice este paso y familiarizarse con el proceso de hello, ya que será necesaria al crear sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="8c8bb-153">Azure AD emite tooonly tokens conocida las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="8c8bb-154">Para poder usar Azure AD desde la aplicación, debe toocreate una entrada para él en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="8c8bb-155">tooregister una nueva aplicación en su inquilino:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="8c8bb-156">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8c8bb-157">En la barra superior de hello, haga clic en su cuenta.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-157">On hello top bar, click your account.</span></span> <span data-ttu-id="8c8bb-158">Hola **Directory** elija inquilino hello Azure AD en el que desea tooregister la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="8c8bb-159">Haga clic en **más servicios** en Hola panel izquierdo y, a continuación, seleccione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="8c8bb-160">Haga clic en **Registros de aplicaciones** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="8c8bb-161">Siga las indicaciones de Hola y crear un **aplicación cliente nativa**.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="8c8bb-162">(Aunque las aplicaciones Cordova están basadas en HTML, aquí estamos creando una aplicación cliente nativa.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="8c8bb-163">Hola **aplicación cliente nativa** opción debe estar seleccionada o aplicación hello no funcionará.)</span><span class="sxs-lookup"><span data-stu-id="8c8bb-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="8c8bb-164">**Nombre** describe su toousers de aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="8c8bb-165">**URI de redireccionamiento** es hello URI que se usa tooreturn tokens tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="8c8bb-166">Escriba **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="8c8bb-167">Cuando termine de registro, Azure AD le asigna una aplicación de tooyour de Id. de aplicación exclusivo.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="8c8bb-168">Necesitará este valor en las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="8c8bb-169">Puede encontrarlo en pestaña de aplicación Hola de Hola que acaba de crear aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="8c8bb-170">toorun `DirSearchClient Sample`, conceder Hola recién creado aplicación permiso tooquery hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="8c8bb-171">De hello **configuración** página, seleccione **permisos necesarios**y, a continuación, seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="8c8bb-172">Para aplicaciones de Azure Active Directory de hello, seleccione **Microsoft Graph** como Hola API y agregar hello **obtener acceso al directorio de hello como usuario con sesión iniciada hello** permiso en **delegados Permisos**.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="8c8bb-173">Esto permite que su Hola de tooquery aplicación API Graph para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="8c8bb-174">Paso 2: Clonar el repositorio de aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="8c8bb-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="8c8bb-175">Desde el shell o la línea de comandos, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="8c8bb-176">Paso 3: Crear la aplicación de Cordova hello</span><span class="sxs-lookup"><span data-stu-id="8c8bb-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="8c8bb-177">Hay varias aplicaciones de Cordova toocreate de formas.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="8c8bb-178">En este tutorial, vamos a usar la interfaz de línea de comandos de hello Cordova (CLI).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="8c8bb-179">Desde el shell o la línea de comandos, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="8c8bb-180">Ese comando crea la estructura de carpetas de Hola y scaffolding de proyecto de Cordova Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="8c8bb-181">Mover la nueva carpeta de DirSearchClient de toohello:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="8c8bb-182">Copiar el contenido de Hola Hola del proyecto de inicio en la subcarpeta de hello World Wide Web mediante un administrador de archivos u Hola siguiente comando en el shell:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="8c8bb-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="8c8bb-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="8c8bb-185">Agregar lista aprobada de hello complemento.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="8c8bb-186">Esto es necesario para invocar Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="8c8bb-187">Agregue todas las plataformas de Hola que desea toosupport.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="8c8bb-188">toohave un ejemplo funcional, deberá tooexecute al menos uno de hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="8c8bb-189">Tenga en cuenta que no puede tooemulate capaz de iOS en Windows o emular Windows en un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="8c8bb-190">Agregue hello AAL para el proyecto de complemento tooyour Cordova:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="8c8bb-191">Paso 4: Agregar código tooauthenticate usuarios y obtener tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c8bb-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="8c8bb-192">aplicación de Hola que va a desarrollar en este tutorial proporcionará una característica de búsqueda de directorio sencillo.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="8c8bb-193">usuario Hola puede, a continuación, escriba el alias de Hola de cualquier usuario en el directorio de Hola y visualizar algunos atributos básicos.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="8c8bb-194">proyecto de inicio de Hello contiene la definición de Hola de interfaz de usuario básica de saludo de la aplicación hello (en www/index.html) y scaffolding de Hola que conecta los eventos de aplicación básico ciclos, enlaces de la interfaz de usuario y los resultados de la lógica de presentación (en www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="8c8bb-195">Hello única tarea que queda para usted es tooadd Hola lógica que implementa las tareas de identidad.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="8c8bb-196">Hello en primer lugar deberá toodo en el código es introducir los valores de protocolo de Hola que Azure AD usa para identificar la aplicación y Hola recursos de destino.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="8c8bb-197">Dichos valores serán solicitudes de token de hello tooconstruct usado más adelante.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="8c8bb-198">Inserte Hola siguiente fragmento de código al principio de hello del archivo de index.js de hello:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="8c8bb-199">Hola `redirectUri` y `clientId` valores deben coincidir con los valores de hello que describen la aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="8c8bb-200">Los de hello encontrará **configurar** ficha Hola portal de Azure, tal como se describe en el paso 1 anteriormente en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="8c8bb-201">Si ha optado por no registrar una nueva aplicación en su propio inquilino, simplemente puede pegar valores de hello preconfigurado tal cual.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="8c8bb-202">A continuación, puede ver ejecutando de ejemplo de Hola, aunque siempre se debe crear su propia entrada para las aplicaciones que están diseñadas para entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="8c8bb-203">A continuación, agregue el código de la solicitud de token de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-203">Next, add hello token request code.</span></span> <span data-ttu-id="8c8bb-204">Insertar Hola siguiente fragmento de código entre hello `search` y `renderData` definiciones:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="8c8bb-205">Examinemos esa función dividiéndola en dos partes principales.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="8c8bb-206">Este ejemplo es toowork diseñada con todos los inquilinos, como opuesto toobeing había vinculada tooa uno determinado.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="8c8bb-207">Usa Hola "/ comunes" punto de conexión, que permite cualquier cuenta de hello tooenter de usuario en tiempo de autenticación y dirige el inquilino de hello solicitud toohello donde pertenece.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="8c8bb-208">Esta primera parte del método hello inspecciona Hola caché AAL toosee si ya se almacena un token.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="8c8bb-209">Si es así, método hello usa a los inquilinos de Hola procedencia de token de Hola para reinicializar AAL.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="8c8bb-210">Esto es necesario tooavoid mensajes adicionales, porque Hola uso de "/ comunes" siempre da lugar a pedir Hola usuario tooenter una nueva cuenta.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="8c8bb-211">segunda parte del método hello de Hello realiza la solicitud de token adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="8c8bb-212">Hola `acquireTokenSilentAsync` método pide AAL tooreturn un token de hello especificada recursos sin mostrar ninguna UX.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="8c8bb-213">Que puede producirse si caché Hola ya tiene un token de acceso adecuado almacenado, o si un token de actualización se puede usa tooget un nuevo token de acceso sin mostrar ningún mensaje.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="8c8bb-214">Si no lo consigue, se reviertan `acquireTokenAsync`--visiblemente que solicitará hello tooauthenticate de usuario.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="8c8bb-215">Ahora que tenemos token hello, finalmente podemos invocar Hola API Graph y realizar consultas de búsqueda de Hola que queremos.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="8c8bb-216">Insertar Hola siguiente fragmento de código siguiente hello `authenticate` definición:</span><span class="sxs-lookup"><span data-stu-id="8c8bb-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="8c8bb-217">archivos de punto de partida de Hello proporcionar experiencia del usuario simple para escribir el alias del usuario en un cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="8c8bb-218">Este método utiliza ese valor tooconstruct una consulta, combinarla con el token de acceso de hello, enviar tooMicrosoft gráfico y analizar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="8c8bb-219">Hola `renderData` método, ya está presente en el archivo de punto de partida de hello, se encarga de visualizar los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="8c8bb-220">Paso 5: Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="8c8bb-220">Step 5: Run hello app</span></span>
<span data-ttu-id="8c8bb-221">La aplicación es toorun llegado el momento.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="8c8bb-222">Resulte sencillo: cuando se inicia la aplicación hello, escriba Hola alias del usuario de hello desea toolook y, a continuación, haga clic en botón Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="8c8bb-223">Se le pedirá que se autentique.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-223">You're prompted for authentication.</span></span> <span data-ttu-id="8c8bb-224">Tras la autenticación correcta y búsqueda correcta, se muestran los atributos de Hola de hello buscada usuario.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="8c8bb-225">Las ejecuciones posteriores llevará a cabo búsqueda Hola sin mostrar ningún mensaje, gracias toohello presencia de hello previamente adquiere token en memoria caché.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="8c8bb-226">pasos concretos de Hola para ejecutar la aplicación hello varían según la plataforma.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="8c8bb-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="8c8bb-227">Windows 10</span></span>
   <span data-ttu-id="8c8bb-228">Tableta/PC: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="8c8bb-229">Dispositivo móvil (requiere una tooa de dispositivo conectado PC de Windows 10 Mobile):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c8bb-230">Durante el saludo ejecuta por primera vez, podría se te pedirán toosign en una licencia de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="8c8bb-231">Para más información, consulte el artículo sobre la [licencia de desarrollador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="8c8bb-232">Tableta/PC con Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8c8bb-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="8c8bb-233">Durante el saludo ejecuta por primera vez, podría se te pedirán toosign en una licencia de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="8c8bb-234">Para más información, consulte el artículo sobre la [licencia de desarrollador](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="8c8bb-235">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="8c8bb-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="8c8bb-236">toorun en un dispositivo conectado:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="8c8bb-237">toorun en el emulador de hello predeterminado:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="8c8bb-238">Use `cordova run windows --list -- --phone` toosee todos los destinos disponibles y `cordova run windows --target=<target_name> -- --phone` toorun aplicación de hello en un emulador o dispositivo específico (por ejemplo, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="8c8bb-239">Android</span><span class="sxs-lookup"><span data-stu-id="8c8bb-239">Android</span></span>
   <span data-ttu-id="8c8bb-240">toorun en un dispositivo conectado:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="8c8bb-241">toorun en el emulador de hello predeterminado:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="8c8bb-242">Asegúrese de que ha creado una instancia del emulador mediante el administrador AVD, tal y como se describió anteriormente en la sección "Requisitos previos" Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="8c8bb-243">Use `cordova run android --list` toosee todos los destinos disponibles y `cordova run android --target=<target_name>` toorun aplicación de hello en un emulador o dispositivo específico (por ejemplo, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="8c8bb-244">iOS</span><span class="sxs-lookup"><span data-stu-id="8c8bb-244">iOS</span></span>
   <span data-ttu-id="8c8bb-245">toorun en un dispositivo conectado:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="8c8bb-246">toorun en el emulador de hello predeterminado:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="8c8bb-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c8bb-247">Asegúrese de que tienen hello `ios-sim` toorun paquete instalado en el emulador de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="8c8bb-248">Para obtener más información, vea Hola "requisitos previos" sección.</span><span class="sxs-lookup"><span data-stu-id="8c8bb-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="8c8bb-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c8bb-249">Next steps</span></span>
<span data-ttu-id="8c8bb-250">Como referencia, está disponible en el ejemplo de Hola finalizado (sin los valores de configuración) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="8c8bb-251">Puede que ahora los escenarios de movimiento en toomore avanzada (y más interesantes).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="8c8bb-252">Es recomendable tootry: [proteger una API Web de Node.js con Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8c8bb-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
