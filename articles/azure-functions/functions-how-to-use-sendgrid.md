---
title: Uso de SendGrid en Azure Functions | Microsoft Docs
description: "Muestra cómo usar SendGrid en Azure Functions"
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
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="71b4b-103">Uso de SendGrid en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="71b4b-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="71b4b-104">Información general sobre SendGrid</span><span class="sxs-lookup"><span data-stu-id="71b4b-104">SendGrid Overview</span></span>

<span data-ttu-id="71b4b-105">Azure Functions admite enlaces de salida de SendGrid para permitir a sus funciones enviar mensajes de correo electrónico con unas cuantas líneas de código y una cuenta de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="71b4b-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="71b4b-106">Para usar la API de SendGrid en una función de Azure, debe tener una [cuenta de SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="71b4b-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="71b4b-107">Además, debe tener una clave de API de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="71b4b-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="71b4b-108">Inicie sesión en la cuenta de SendGrid y haga clic en **Settings** (Configuración) y luego en **API Key** (Clave de API) para generar una clave de API.</span><span class="sxs-lookup"><span data-stu-id="71b4b-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="71b4b-109">Tenga a mano la clave, porque debe usarla en un próximo paso.</span><span class="sxs-lookup"><span data-stu-id="71b4b-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="71b4b-110">Ahora está listo para crear una Function App de Azure.</span><span class="sxs-lookup"><span data-stu-id="71b4b-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="71b4b-111">Creación de una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="71b4b-111">Create an Azure Function app</span></span> 

<span data-ttu-id="71b4b-112">Las Function App de Azure son contenedores para una o varias funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="71b4b-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="71b4b-113">Las funciones de Azure son justamente eso: una función.</span><span class="sxs-lookup"><span data-stu-id="71b4b-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="71b4b-114">Cada función de Azure está asociada a un desencadenador, que es un evento que hace que la función se ejecute.</span><span class="sxs-lookup"><span data-stu-id="71b4b-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="71b4b-115">Cada función puede contener cualquier número de enlaces de entrada o salida.</span><span class="sxs-lookup"><span data-stu-id="71b4b-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="71b4b-116">Los enlaces son servicios que puede usar en una función.</span><span class="sxs-lookup"><span data-stu-id="71b4b-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="71b4b-117">SendGrid es un enlace de salida que se puede usar para enviar correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="71b4b-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="71b4b-118">Inicie sesión en Azure Portal y [cree una Function App de Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) o abra una Function App existente.</span><span class="sxs-lookup"><span data-stu-id="71b4b-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="71b4b-119">Cree una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="71b4b-119">Create an Azure function.</span></span> <span data-ttu-id="71b4b-120">Para simplificarla, elija un desencadenador manual y C#.</span><span class="sxs-lookup"><span data-stu-id="71b4b-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Creación de una función de Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="71b4b-122">Configuración de SendGrid para usarlo en una Function App de Azure</span><span class="sxs-lookup"><span data-stu-id="71b4b-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="71b4b-123">Debe almacenar la clave de API de SendGrid como una configuración de aplicación para utilizarla en una función.</span><span class="sxs-lookup"><span data-stu-id="71b4b-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="71b4b-124">El campo ApiKey no es la clave de API de SendGrid real, sino un valor de configuración de la aplicación que se establece y que representa la clave de API real.</span><span class="sxs-lookup"><span data-stu-id="71b4b-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="71b4b-125">La clave se almacena de esta forma por seguridad, ya que es independiente de cualquier código o archivo que pueda comprobarse en el control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="71b4b-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="71b4b-126">Cree una clave **AppSettings** en la **configuración de la aplicación** de la Function App.</span><span class="sxs-lookup"><span data-stu-id="71b4b-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Creación de una función de Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="71b4b-128">Configuración de enlaces de salida de SendGrid</span><span class="sxs-lookup"><span data-stu-id="71b4b-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="71b4b-129">SendGrid está disponible como un enlace de salida de una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="71b4b-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="71b4b-130">Para crear un enlace de salida de SendGrid:</span><span class="sxs-lookup"><span data-stu-id="71b4b-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="71b4b-131">Vaya a la pestaña **Integrar** de la función en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="71b4b-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="71b4b-132">Haga clic en **Nueva salida** para crear un enlace de salida de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="71b4b-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="71b4b-133">Rellene las propiedades **Clave de API** y **Nombre de parámetro de mensaje**.</span><span class="sxs-lookup"><span data-stu-id="71b4b-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="71b4b-134">Si lo desea, puede especificar las demás propiedades ahora o, en su lugar, también puede codificarlas.</span><span class="sxs-lookup"><span data-stu-id="71b4b-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="71b4b-135">Esta configuración se puede utilizar como valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="71b4b-135">These settings can be used as defaults.</span></span>

 ![Configuración de enlaces de salida de SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="71b4b-137">Al agregar un enlace a una función se crea un archivo denominado **function.json** en la carpeta de la función.</span><span class="sxs-lookup"><span data-stu-id="71b4b-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="71b4b-138">Este archivo contiene la misma información que se ve en la pestaña **Integrar** de la función de Azure, pero en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="71b4b-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="71b4b-139">Al especificar los campos **ApiKey**, **mensaje** y **de**, se crean las entradas siguientes en el archivo **function.json**:</span><span class="sxs-lookup"><span data-stu-id="71b4b-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

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

<span data-ttu-id="71b4b-140">Si lo prefiere, puede modificar este archivo por sí mismo directamente.</span><span class="sxs-lookup"><span data-stu-id="71b4b-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="71b4b-141">Ahora que ha creado y configurado la Function App y la función, puede escribir el código para enviar un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="71b4b-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="71b4b-142">Escritura del código que crea y envía correos electrónicos</span><span class="sxs-lookup"><span data-stu-id="71b4b-142">Write code that creates and sends email</span></span>

<span data-ttu-id="71b4b-143">La API de SendGrid contiene todos los comandos que necesita para crear y enviar un correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="71b4b-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="71b4b-144">Reemplace el código de la función por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="71b4b-144">Replace the code in the function with the following code:</span></span>

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
    // change to email of recipient
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

<span data-ttu-id="71b4b-145">Observe que la primera línea contiene la directiva ```#r``` que hace referencia al ensamblado de SendGrid.</span><span class="sxs-lookup"><span data-stu-id="71b4b-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="71b4b-146">Después, puede usar una instrucción ```using``` para acceder con más facilidad a los objetos de ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="71b4b-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="71b4b-147">En el código, cree instancias de los objetos ```Mail```, ```Personalization``` y ```Content``` a través de la API de SendGrid que redacta el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="71b4b-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="71b4b-148">Cuando devuelve el mensaje, SendGrid lo entrega.</span><span class="sxs-lookup"><span data-stu-id="71b4b-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="71b4b-149">La firma de la función contiene también un parámetro de salida adicional del tipo ```Mail``` denominado ```message```.</span><span class="sxs-lookup"><span data-stu-id="71b4b-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="71b4b-150">Tanto los enlaces de entrada como los de salida se expresan como parámetros de la función en el código.</span><span class="sxs-lookup"><span data-stu-id="71b4b-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="71b4b-151">Pruebe el código; para ello, haga clic en **Probar** y escriba un mensaje en el campo **Cuerpo de la solicitud** y luego haga clic en el botón **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="71b4b-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![Prueba del código](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="71b4b-153">Compruebe el correo electrónico para verificar que SendGrid envió el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="71b4b-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="71b4b-154">Debe remitirse a la dirección del código del paso 1 y contener el mensaje escrito en el campo **Cuerpo de la solicitud**.</span><span class="sxs-lookup"><span data-stu-id="71b4b-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71b4b-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71b4b-155">Next steps</span></span>
<span data-ttu-id="71b4b-156">En este artículo se ha explicado cómo usar el servicio SendGrid para crear y enviar correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="71b4b-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="71b4b-157">Para más información sobre el uso de Azure Functions en sus aplicaciones, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="71b4b-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="71b4b-158">[Procedimientos recomendados de Azure Functions](functions-best-practices.md): se enumeran algunos procedimientos recomendados para crear Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="71b4b-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="71b4b-159">[Guía para desarrolladores de Azure Functions](functions-reference.md): contiene las referencias del programador para codificar las funciones y definir los desencadenadores y los enlaces.</span><span class="sxs-lookup"><span data-stu-id="71b4b-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="71b4b-160">[Prueba de Azure Functions](functions-test-a-function.md): se describen las diversas herramientas y técnicas para probar sus funciones.</span><span class="sxs-lookup"><span data-stu-id="71b4b-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>