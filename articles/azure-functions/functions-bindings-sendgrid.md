---
title: enlaces de funciones SendGrid aaaAzure | Documentos de Microsoft
description: Referencia de enlaces de SendGrid de Azure Functions
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Enlaces de SendGrid de Azure Functions

Este artículo se explica cómo tooconfigure y trabajar con enlaces de SendGrid en las funciones de Azure. Con SendGrid, puede utilizar correo electrónico de las funciones de Azure toosend personalizado mediante programación.

Este artículo sirve como información de referencia para los desarrolladores de Azure Functions. Si está nuevas funciones de tooAzure, empiece con hello recursos siguientes:

[Cree la primera Azure Function](functions-create-first-azure-function.md). 
Referencias para desarrolladores de [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) o [nodo](functions-reference-node.md).

## <a name="functionjson-for-sendgrid-bindings"></a>function.json para enlaces de SendGrid

Azure Functions proporciona un enlace de salida para SendGrid. Hola SendGrid salida enlace permite toocreate y enviar correo electrónico mediante programación. 

enlace de SendGrid Hola admite Hola propiedades siguientes:

- `name`: Es obligatorio - Nombre de variable de saludo utilizado en código de la función para la solicitud de Hola o cuerpo de la solicitud. Este valor es ```$return``` cuando hay solo un valor de devuelto. 
- `type`: Es obligatorio - debe estar configurado demasiado "sendGrid".
- `direction`: Requerida: debe ser establecido demasiado "out".
- `apiKey`: Requerida: debe ser el nombre de la clave de API que se almacena en la configuración de la aplicación de la aplicación de la función de hello toohello del conjunto de.
- `to`: Hola dirección de correo electrónico del destinatario.
- `from`: Hola dirección de correo electrónico del remitente.
- `subject`: asunto Hola de correo electrónico de Hola.
- `text`: Hola contenido de correo electrónico.

Ejemplo de **function.json**:

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente. Esta acción protege la información confidencial.
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>Enlace de salida de ejemplo de C# de hello SendGrid

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Nodo de hello SendGrid salida de ejemplo para enlazar

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a>Pasos siguientes
Para información sobre otros enlaces y desencadenadores de Azure Functions, consulte: 
- [Referencia para desarrolladores de desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md)

- [Procedimientos recomendados para las funciones de Azure](functions-best-practices.md) enumera algunos toouse de prácticas recomendada al crear funciones de Azure.

- [Guía para desarrolladores de Azure Functions](functions-reference.md): contiene las referencias del programador para codificar las funciones y definir los desencadenadores y los enlaces.
