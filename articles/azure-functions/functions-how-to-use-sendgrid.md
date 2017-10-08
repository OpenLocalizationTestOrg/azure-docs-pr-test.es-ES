---
title: aaaHow toouse SendGrid en las funciones de Azure | Documentos de Microsoft
description: "Muestra cómo toouse SendGrid en las funciones de Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="016a9-103">Cómo toouse SendGrid en las funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="016a9-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="016a9-104">Información general sobre SendGrid</span><span class="sxs-lookup"><span data-stu-id="016a9-104">SendGrid Overview</span></span>

<span data-ttu-id="016a9-105">Azure funciones es compatible con SendGrid habían salida enlaces tooenable los mensajes de correo electrónico de las funciones toosend con unas pocas líneas de código y una cuenta de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="016a9-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="016a9-106">API de SendGrid toouse hello en una función de Azure, debe tener un [cuenta de SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="016a9-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="016a9-107">Además, debe tener una clave de API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="016a9-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="016a9-108">Inicie sesión en la cuenta de SendGrid tooyour y haga clic en **configuración** , a continuación, **clave de API** clave toogenerate una API.</span><span class="sxs-lookup"><span data-stu-id="016a9-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="016a9-109">Tenga a mano la clave, porque debe usarla en un próximo paso.</span><span class="sxs-lookup"><span data-stu-id="016a9-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="016a9-110">Ya estás listo toocreate una aplicación de la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="016a9-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="016a9-111">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="016a9-111">Create an Azure Function app</span></span> 

<span data-ttu-id="016a9-112">Las Function App de Azure son contenedores para una o varias funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="016a9-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="016a9-113">Las funciones de Azure son justamente eso: una función.</span><span class="sxs-lookup"><span data-stu-id="016a9-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="016a9-114">Cada función de Azure es desencadenador tooone relacionados, que es un acontecimiento que provoca Hola función toorun.</span><span class="sxs-lookup"><span data-stu-id="016a9-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="016a9-115">Cada función puede contener cualquier número de enlaces de entrada o salida.</span><span class="sxs-lookup"><span data-stu-id="016a9-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="016a9-116">Los enlaces son servicios que puede usar en una función.</span><span class="sxs-lookup"><span data-stu-id="016a9-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="016a9-117">SendGrid es una salida de enlace puede utilizar el correo electrónico toosend.</span><span class="sxs-lookup"><span data-stu-id="016a9-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="016a9-118">Inicie sesión en el portal de Azure toohello y [crear una aplicación de la función de Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) o abrir una aplicación existente de la función.</span><span class="sxs-lookup"><span data-stu-id="016a9-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="016a9-119">Cree una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="016a9-119">Create an Azure function.</span></span> <span data-ttu-id="016a9-120">tookeep, simple, elija un desencadenador manual y C#.</span><span class="sxs-lookup"><span data-stu-id="016a9-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Creación de una función de Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="016a9-122">Configuración de SendGrid para usarlo en una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="016a9-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="016a9-123">Debe almacenar la clave de API de SendGrid como un toouse de configuración de aplicación en una función.</span><span class="sxs-lookup"><span data-stu-id="016a9-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="016a9-124">Hola ApiKey campo no es la clave de API de SendGrid real, pero definen una configuración de aplicación que representa la clave de API real.</span><span class="sxs-lookup"><span data-stu-id="016a9-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="016a9-125">La clave se almacena de esta forma por seguridad, ya que es independiente de cualquier código o archivo que pueda comprobarse en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="016a9-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="016a9-126">Cree una clave **AppSettings** en la **configuración de la aplicación** de la Function App.</span><span class="sxs-lookup"><span data-stu-id="016a9-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Creación de una función de Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="016a9-128">Configuración de enlaces de salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="016a9-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="016a9-129">SendGrid está disponible como un enlace de salida de una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="016a9-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="016a9-130">toocreate un SendGrid el enlace de salida:</span><span class="sxs-lookup"><span data-stu-id="016a9-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="016a9-131">Vaya toohello **integrar** ficha de función de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="016a9-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="016a9-132">Haga clic en **nueva salida** toocreate un SendGrid el enlace de salida.</span><span class="sxs-lookup"><span data-stu-id="016a9-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="016a9-133">Rellene hello **clave de API** y **nombre de parámetro de mensaje** propiedades.</span><span class="sxs-lookup"><span data-stu-id="016a9-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="016a9-134">Si lo desea, puede escribir Hola ahora otras propiedades, o escriba el código en su lugar.</span><span class="sxs-lookup"><span data-stu-id="016a9-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="016a9-135">Esta configuración se puede utilizar como valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="016a9-135">These settings can be used as defaults.</span></span>

 ![Configuración de enlaces de salida de SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="016a9-137">Agregar una función de enlace tooa crea un archivo denominado **function.json** en la carpeta de la función.</span><span class="sxs-lookup"><span data-stu-id="016a9-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="016a9-138">Este archivo contiene todos Hola la misma información que aparece en hello Azure función **integrar** pestaña, pero en Json de formato.</span><span class="sxs-lookup"><span data-stu-id="016a9-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="016a9-139">Hola configuración **ApiKey**, **mensaje**, y **de** campos crean Hola siguiendo las entradas de hello **function.json** archivo:</span><span class="sxs-lookup"><span data-stu-id="016a9-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="016a9-140">Si lo prefiere, puede modificar este archivo por sí mismo directamente.</span><span class="sxs-lookup"><span data-stu-id="016a9-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="016a9-141">Ahora que ha creado y configurado Hola función aplicación y función, puede escribir Hola código toosend un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="016a9-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="016a9-142">Escritura del código que crea y envía correos electrónicos</span><span class="sxs-lookup"><span data-stu-id="016a9-142">Write code that creates and sends email</span></span>

<span data-ttu-id="016a9-143">Hola SendGrid API contiene todos Hola comandos que necesita toocreate y enviar un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="016a9-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="016a9-144">Reemplace el código de hello en función de hello con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="016a9-144">Replace hello code in hello function with hello following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="016a9-145">Aviso Hola primera línea contiene Hola ```#r``` directiva que hace referencia al ensamblado de SendGrid Hola.</span><span class="sxs-lookup"><span data-stu-id="016a9-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="016a9-146">Después, puede usar un ```using``` toomore instrucción acceder fácilmente a los objetos de hello en ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="016a9-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="016a9-147">En el código de hello, crear instancias de ```Mail```, ```Personalization```, y ```Content``` objetos de hello SendGrid API que redacción correo electrónico Hola.</span><span class="sxs-lookup"><span data-stu-id="016a9-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="016a9-148">Cuando se devuelven mensajes de bienvenida, SendGrid lo entrega.</span><span class="sxs-lookup"><span data-stu-id="016a9-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="016a9-149">Hello firma de función también contiene el parámetro de tipo de salida adicional ```Mail``` denominado ```message```.</span><span class="sxs-lookup"><span data-stu-id="016a9-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="016a9-150">Tanto los enlaces de entrada como los de salida se expresan como parámetros de la función en el código.</span><span class="sxs-lookup"><span data-stu-id="016a9-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="016a9-151">Probar el código, haga clic en **prueba** y escribir un mensaje en hello **cuerpo de la solicitud** campo, a continuación, haga clic en hello **ejecutar** botón.</span><span class="sxs-lookup"><span data-stu-id="016a9-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Prueba del código](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="016a9-153">Compruebe que SendGrid enviar correo electrónico de Hola de tooverify de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="016a9-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="016a9-154">Debe ir toohello dirección en el código de hello del paso 1 y contener el mensaje de saludo de Hola **cuerpo de la solicitud**.</span><span class="sxs-lookup"><span data-stu-id="016a9-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="016a9-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="016a9-155">Next steps</span></span>
<span data-ttu-id="016a9-156">Este artículo demuestra cómo toouse Hola SendGrid servicio toocreate y enviar correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="016a9-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="016a9-157">toolearn más sobre el uso de funciones de Azure en sus aplicaciones, vea Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="016a9-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="016a9-158">[Procedimientos recomendados para las funciones de Azure](functions-best-practices.md) enumera algunos toouse de prácticas recomendada al crear funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="016a9-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="016a9-159">[Guía para desarrolladores de Azure Functions](functions-reference.md): contiene las referencias del programador para codificar las funciones y definir los desencadenadores y los enlaces.</span><span class="sxs-lookup"><span data-stu-id="016a9-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="016a9-160">[Prueba de Azure Functions](functions-test-a-function.md): se describen las diversas herramientas y técnicas para probar sus funciones.</span><span class="sxs-lookup"><span data-stu-id="016a9-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>