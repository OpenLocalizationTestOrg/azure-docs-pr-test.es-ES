---
title: "aaaAzure AD v2 iOS introducción - el programa de instalación | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones de iOS (Swift) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="22f92-103">Configuración de la aplicación de iOS</span><span class="sxs-lookup"><span data-stu-id="22f92-103">Setting up your iOS application</span></span>

<span data-ttu-id="22f92-104">Esta sección proporciona instrucciones paso a paso acerca de cómo toocreate un nuevo toodemonstrate proyecto cómo toointegrate una aplicación de iOS (Swift) con *inicie sesión con Microsoft* para que pueden consultar las API Web que requieran un token.</span><span class="sxs-lookup"><span data-stu-id="22f92-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="22f92-105">¿Prefiere toodownload proyecto de XCode de este ejemplo en su lugar?</span><span class="sxs-lookup"><span data-stu-id="22f92-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="22f92-106">[Descargar un proyecto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.</span><span class="sxs-lookup"><span data-stu-id="22f92-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="22f92-107">Instalar toodownload Carthage y generar MSAL</span><span class="sxs-lookup"><span data-stu-id="22f92-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="22f92-108">Se utiliza el Administrador de paquetes Carthage durante el período de vista previa de Hola de MSAL: se integra con XCode manteniendo la capacidad de hello para la biblioteca de Microsoft toomake cambios toohello.</span><span class="sxs-lookup"><span data-stu-id="22f92-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="22f92-109">Descargue e instale la versión más reciente de Hola de Carthage [aquí](https://github.com/Carthage/Carthage/releases "Carthage dirección URL de descarga")</span><span class="sxs-lookup"><span data-stu-id="22f92-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="22f92-110">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="22f92-110">Creating your application</span></span>

1.  <span data-ttu-id="22f92-111">Abra Xcode y seleccione `Create a new Xcode project`.</span><span class="sxs-lookup"><span data-stu-id="22f92-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="22f92-112">Seleccione `iOS` > `Single view Application` y haga clic en *Siguiente*</span><span class="sxs-lookup"><span data-stu-id="22f92-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="22f92-113">Asigne un nombre al producto y haga clic en *Siguiente*</span><span class="sxs-lookup"><span data-stu-id="22f92-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="22f92-114">Seleccione una carpeta toocreate la aplicación y haga clic en *crear*</span><span class="sxs-lookup"><span data-stu-id="22f92-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="22f92-115">Compilar hello MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="22f92-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="22f92-116">Siga las instrucciones de hello debajo toopull y, a continuación, compilar la versión más reciente de Hola de bibliotecas MSAL mediante Carthage:</span><span class="sxs-lookup"><span data-stu-id="22f92-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="22f92-117">Abra terminal de bash hello y vaya carpeta raíz de la aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="22f92-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="22f92-118">Hola debajo de copiar y pegar en hello bash terminal toocreate un archivo de 'Cartfile':</span><span class="sxs-lookup"><span data-stu-id="22f92-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="22f92-119">Copie y pegue Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="22f92-119">Copy and paste hello below.</span></span> <span data-ttu-id="22f92-120">Este comando captura las dependencias en una carpeta Carthage/desprotecciones y, a continuación, compila la biblioteca de Hola MSAL:</span><span class="sxs-lookup"><span data-stu-id="22f92-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="22f92-121">proceso de Hello anterior es toodownload usado y compilación Hola biblioteca de autenticación de Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="22f92-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="22f92-122">MSAL controla la adquisición, almacenamiento en caché y actualizar usuario tooaccess de tokens que se usan las API protegidas por hello Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="22f92-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="22f92-123">Agregar aplicación de hello MSAL framework tooyour</span><span class="sxs-lookup"><span data-stu-id="22f92-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="22f92-124">En Xcode, abra hello `General` ficha</span><span class="sxs-lookup"><span data-stu-id="22f92-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="22f92-125">Vaya toohello `Linked Frameworks and Libraries` sección y haga clic en`+`</span><span class="sxs-lookup"><span data-stu-id="22f92-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="22f92-126">Seleccionar `Add other…`</span><span class="sxs-lookup"><span data-stu-id="22f92-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="22f92-127">Seleccione: `Carthage` > `Build` > `iOS` > `MSAL.framework` y haga clic en *Abrir*.</span><span class="sxs-lookup"><span data-stu-id="22f92-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="22f92-128">Debería ver `MSAL.framework` agregado toohello lista.</span><span class="sxs-lookup"><span data-stu-id="22f92-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="22f92-129">Vaya demasiado`Build Phases` ficha y haga clic en `+` icono, elegir`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="22f92-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="22f92-130">Agregar Hola después contenido toohello *script área*:</span><span class="sxs-lookup"><span data-stu-id="22f92-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="22f92-131">Agregue la Hola siguiente demasiado<code>Input Files</code> haciendo clic en <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="22f92-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="22f92-132">Creación de la interfaz de usuario de la aplicación</span><span class="sxs-lookup"><span data-stu-id="22f92-132">Creating your application’s UI</span></span>
<span data-ttu-id="22f92-133">Debe crearse un archivo Main.storyboard automáticamente como parte de la plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="22f92-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="22f92-134">Siga las instrucciones de Hola por debajo de la aplicación de hello toocreate interfaz de usuario:</span><span class="sxs-lookup"><span data-stu-id="22f92-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="22f92-135">Control + clic `Main.storyboard` toobring una copia de seguridad del menú contextual hello y, a continuación, haga clic en:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="22f92-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="22f92-136">Reemplace hello `<scenes>` nodo con el código de hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="22f92-136">Replace hello `<scenes>` node with hello code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
