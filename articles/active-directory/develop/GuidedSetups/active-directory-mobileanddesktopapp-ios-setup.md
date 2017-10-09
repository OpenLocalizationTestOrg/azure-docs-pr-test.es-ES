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
## <a name="setting-up-your-ios-application"></a>Configuración de la aplicación de iOS

Esta sección proporciona instrucciones paso a paso acerca de cómo toocreate un nuevo toodemonstrate proyecto cómo toointegrate una aplicación de iOS (Swift) con *inicie sesión con Microsoft* para que pueden consultar las API Web que requieran un token.

> ¿Prefiere toodownload proyecto de XCode de este ejemplo en su lugar? [Descargar un proyecto](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.


## <a name="install-carthage-toodownload-and-build-msal"></a>Instalar toodownload Carthage y generar MSAL
Se utiliza el Administrador de paquetes Carthage durante el período de vista previa de Hola de MSAL: se integra con XCode manteniendo la capacidad de hello para la biblioteca de Microsoft toomake cambios toohello.

- Descargue e instale la versión más reciente de Hola de Carthage [aquí](https://github.com/Carthage/Carthage/releases "Carthage dirección URL de descarga")

## <a name="creating-your-application"></a>Creación de la aplicación

1.  Abra Xcode y seleccione `Create a new Xcode project`.
2.  Seleccione `iOS` > `Single view Application` y haga clic en *Siguiente*
3.  Asigne un nombre al producto y haga clic en *Siguiente*
4.  Seleccione una carpeta toocreate la aplicación y haga clic en *crear*

## <a name="build-hello-msal-framework"></a>Compilar hello MSAL Framework

Siga las instrucciones de hello debajo toopull y, a continuación, compilar la versión más reciente de Hola de bibliotecas MSAL mediante Carthage:

1.  Abra terminal de bash hello y vaya carpeta raíz de la aplicación toohello
2.  Hola debajo de copiar y pegar en hello bash terminal toocreate un archivo de 'Cartfile':

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Copie y pegue Hola siguiente. Este comando captura las dependencias en una carpeta Carthage/desprotecciones y, a continuación, compila la biblioteca de Hola MSAL:
</li>
</ol>

```bash
carthage update
```

> proceso de Hello anterior es toodownload usado y compilación Hola biblioteca de autenticación de Microsoft (MSAL). MSAL controla la adquisición, almacenamiento en caché y actualizar usuario tooaccess de tokens que se usan las API protegidas por hello Azure Active Directory v2.

## <a name="add-hello-msal-framework-tooyour-application"></a>Agregar aplicación de hello MSAL framework tooyour
1.  En Xcode, abra hello `General` ficha
2.  Vaya toohello `Linked Frameworks and Libraries` sección y haga clic en`+`
3.  Seleccionar `Add other…`
4.  Seleccione: `Carthage` > `Build` > `iOS` > `MSAL.framework` y haga clic en *Abrir*. Debería ver `MSAL.framework` agregado toohello lista.
5.  Vaya demasiado`Build Phases` ficha y haga clic en `+` icono, elegir`New Run Script Phase`
6.  Agregar Hola después contenido toohello *script área*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Agregue la Hola siguiente demasiado<code>Input Files</code> haciendo clic en <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Creación de la interfaz de usuario de la aplicación
Debe crearse un archivo Main.storyboard automáticamente como parte de la plantilla de proyecto. Siga las instrucciones de Hola por debajo de la aplicación de hello toocreate interfaz de usuario:

1.  Control + clic `Main.storyboard` toobring una copia de seguridad del menú contextual hello y, a continuación, haga clic en:`Open As` > `Source Code`
2.  Reemplace hello `<scenes>` nodo con el código de hello siguiente:

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
