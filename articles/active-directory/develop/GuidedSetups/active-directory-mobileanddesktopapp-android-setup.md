---
title: "aaaAzure AD v2 Android introducción - el programa de instalación | Documentos de Microsoft"
description: "Cómo puede una aplicación de Android obtener un token de acceso y llamar a las API Graph que requieren tokens de acceso desde el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurar su proyecto

> ¿Prefiere toodownload proyecto de Android Studio de este ejemplo en su lugar? [Descargar un proyecto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.


### <a name="create-a-new-project"></a>Crear un nuevo proyecto 
1.  Abra Android Studio, vaya a `File` > `New` > `New Project`.
2.  Asigne un nombre a la aplicación y haga clic en `Next`.
3.  Asegúrese de que tooselect *API 21 o posterior (Android 5.0)* y haga clic en`Next`
4.  Salga de `Empty Activity`, haga clic en `Next` y luego en `Finish`.


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Agregar proyecto de hello biblioteca de autenticación de Microsoft (MSAL) tooyour
1.  En Android Studio, vaya a `Gradle Scripts` > `build.gradle (Module: app)`.
2.  Copiar y pegar siguiente de hello código en `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>Acerca de este paquete

paquete de Hello anterior instala Hola biblioteca de autenticación de Microsoft (MSAL). MSAL controla la adquisición, almacenamiento en caché y actualizar usuario tooaccess de tokens que se usan las API protegidas por el punto de conexión de Azure Active Directory v2.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>Creación de la IU de la aplicación

1.  Abra `activity_main.xml` en `res` > `layout`.
2.  Cambiar el diseño de actividad de hello `android.support.constraint.ConstraintLayout` u otros demasiado`LinearLayout`
3.  Agregar `android:orientation="vertical"` propiedad demasiado`LinearLayout` nodo
4.  Código de copiar y pegar siguiente de hello en hello `LinearLayout` nodo, reemplazando el contenido actual de hello:

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

