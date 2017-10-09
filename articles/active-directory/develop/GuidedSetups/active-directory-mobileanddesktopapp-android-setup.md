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
## <a name="set-up-your-project"></a><span data-ttu-id="c6261-103">Configurar su proyecto</span><span class="sxs-lookup"><span data-stu-id="c6261-103">Set up your project</span></span>

> <span data-ttu-id="c6261-104">¿Prefiere toodownload proyecto de Android Studio de este ejemplo en su lugar?</span><span class="sxs-lookup"><span data-stu-id="c6261-104">Prefer toodownload this sample's Android Studio project instead?</span></span> <span data-ttu-id="c6261-105">[Descargar un proyecto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.</span><span class="sxs-lookup"><span data-stu-id="c6261-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="c6261-106">Crear un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="c6261-106">Create a new project</span></span> 
1.  <span data-ttu-id="c6261-107">Abra Android Studio, vaya a `File` > `New` > `New Project`.</span><span class="sxs-lookup"><span data-stu-id="c6261-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="c6261-108">Asigne un nombre a la aplicación y haga clic en `Next`.</span><span class="sxs-lookup"><span data-stu-id="c6261-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="c6261-109">Asegúrese de que tooselect *API 21 o posterior (Android 5.0)* y haga clic en`Next`</span><span class="sxs-lookup"><span data-stu-id="c6261-109">Make sure tooselect *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="c6261-110">Salga de `Empty Activity`, haga clic en `Next` y luego en `Finish`.</span><span class="sxs-lookup"><span data-stu-id="c6261-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="c6261-111">Agregar proyecto de hello biblioteca de autenticación de Microsoft (MSAL) tooyour</span><span class="sxs-lookup"><span data-stu-id="c6261-111">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1.  <span data-ttu-id="c6261-112">En Android Studio, vaya a `Gradle Scripts` > `build.gradle (Module: app)`.</span><span class="sxs-lookup"><span data-stu-id="c6261-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="c6261-113">Copiar y pegar siguiente de hello código en `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="c6261-113">Copy and paste hello following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="c6261-114">Acerca de este paquete</span><span class="sxs-lookup"><span data-stu-id="c6261-114">About this package</span></span>

<span data-ttu-id="c6261-115">paquete de Hello anterior instala Hola biblioteca de autenticación de Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="c6261-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="c6261-116">MSAL controla la adquisición, almacenamiento en caché y actualizar usuario tooaccess de tokens que se usan las API protegidas por el punto de conexión de Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="c6261-116">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="c6261-117">Creación de la IU de la aplicación</span><span class="sxs-lookup"><span data-stu-id="c6261-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="c6261-118">Abra `activity_main.xml` en `res` > `layout`.</span><span class="sxs-lookup"><span data-stu-id="c6261-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="c6261-119">Cambiar el diseño de actividad de hello `android.support.constraint.ConstraintLayout` u otros demasiado`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="c6261-119">Change hello activity layout from `android.support.constraint.ConstraintLayout` or other too`LinearLayout`</span></span>
3.  <span data-ttu-id="c6261-120">Agregar `android:orientation="vertical"` propiedad demasiado`LinearLayout` nodo</span><span class="sxs-lookup"><span data-stu-id="c6261-120">Add `android:orientation="vertical"` property too`LinearLayout` node</span></span>
4.  <span data-ttu-id="c6261-121">Código de copiar y pegar siguiente de hello en hello `LinearLayout` nodo, reemplazando el contenido actual de hello:</span><span class="sxs-lookup"><span data-stu-id="c6261-121">Copy and paste hello following code into hello `LinearLayout` node, replacing hello current content:</span></span>

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

