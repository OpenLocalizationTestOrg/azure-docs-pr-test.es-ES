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
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Cómo toouse SendGrid en las funciones de Azure

## <a name="sendgrid-overview"></a>Información general sobre SendGrid

Azure funciones es compatible con SendGrid habían salida enlaces tooenable los mensajes de correo electrónico de las funciones toosend con unas pocas líneas de código y una cuenta de SendGrid.

API de SendGrid toouse hello en una función de Azure, debe tener un [cuenta de SendGrid](http://SendGrid.com). Además, debe tener una clave de API de SendGrid. Inicie sesión en la cuenta de SendGrid tooyour y haga clic en **configuración** , a continuación, **clave de API** clave toogenerate una API. Tenga a mano la clave, porque debe usarla en un próximo paso.

Ya estás listo toocreate una aplicación de la función de Azure.

## <a name="create-an-azure-function-app"></a>Creación de una Function App de Azure 

Las Function App de Azure son contenedores para una o varias funciones de Azure. Las funciones de Azure son justamente eso: una función. Cada función de Azure es desencadenador tooone relacionados, que es un acontecimiento que provoca Hola función toorun.
Cada función puede contener cualquier número de enlaces de entrada o salida. Los enlaces son servicios que puede usar en una función. SendGrid es una salida de enlace puede utilizar el correo electrónico toosend. 

1. Inicie sesión en el portal de Azure toohello y [crear una aplicación de la función de Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) o abrir una aplicación existente de la función. 
2. Cree una función de Azure. tookeep, simple, elija un desencadenador manual y C#. 

 ![Creación de una función de Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>Configuración de SendGrid para usarlo en una Function App de Azure

Debe almacenar la clave de API de SendGrid como un toouse de configuración de aplicación en una función. Hola ApiKey campo no es la clave de API de SendGrid real, pero definen una configuración de aplicación que representa la clave de API real. La clave se almacena de esta forma por seguridad, ya que es independiente de cualquier código o archivo que pueda comprobarse en el control de código fuente.

- Cree una clave **AppSettings** en la **configuración de la aplicación** de la Function App.

 ![Creación de una función de Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>Configuración de enlaces de salida de SendGrid

SendGrid está disponible como un enlace de salida de una función de Azure. toocreate un SendGrid el enlace de salida:

1. Vaya toohello **integrar** ficha de función de Hola Hola portal de Azure.
2. Haga clic en **nueva salida** toocreate un SendGrid el enlace de salida.
3. Rellene hello **clave de API** y **nombre de parámetro de mensaje** propiedades. Si lo desea, puede escribir Hola ahora otras propiedades, o escriba el código en su lugar. Esta configuración se puede utilizar como valores predeterminados.

 ![Configuración de enlaces de salida de SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Agregar una función de enlace tooa crea un archivo denominado **function.json** en la carpeta de la función. Este archivo contiene todos Hola la misma información que aparece en hello Azure función **integrar** pestaña, pero en Json de formato. Hola configuración **ApiKey**, **mensaje**, y **de** campos crean Hola siguiendo las entradas de hello **function.json** archivo: 

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

Si lo prefiere, puede modificar este archivo por sí mismo directamente.

Ahora que ha creado y configurado Hola función aplicación y función, puede escribir Hola código toosend un correo electrónico.

## <a name="write-code-that-creates-and-sends-email"></a>Escritura del código que crea y envía correos electrónicos

Hola SendGrid API contiene todos Hola comandos que necesita toocreate y enviar un correo electrónico.  

- Reemplace el código de hello en función de hello con hello siguiente código:

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

Aviso Hola primera línea contiene Hola ```#r``` directiva que hace referencia al ensamblado de SendGrid Hola. Después, puede usar un ```using``` toomore instrucción acceder fácilmente a los objetos de hello en ese espacio de nombres. En el código de hello, crear instancias de ```Mail```, ```Personalization```, y ```Content``` objetos de hello SendGrid API que redacción correo electrónico Hola. Cuando se devuelven mensajes de bienvenida, SendGrid lo entrega. 

Hello firma de función también contiene el parámetro de tipo de salida adicional ```Mail``` denominado ```message```. Tanto los enlaces de entrada como los de salida se expresan como parámetros de la función en el código. 

2. Probar el código, haga clic en **prueba** y escribir un mensaje en hello **cuerpo de la solicitud** campo, a continuación, haga clic en hello **ejecutar** botón.

 ![Prueba del código](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. Compruebe que SendGrid enviar correo electrónico de Hola de tooverify de correo electrónico. Debe ir toohello dirección en el código de hello del paso 1 y contener el mensaje de saludo de Hola **cuerpo de la solicitud**.

## <a name="next-steps"></a>Pasos siguientes
Este artículo demuestra cómo toouse Hola SendGrid servicio toocreate y enviar correo electrónico. toolearn más sobre el uso de funciones de Azure en sus aplicaciones, vea Hola temas siguientes: 

- [Procedimientos recomendados para las funciones de Azure](functions-best-practices.md) enumera algunos toouse de prácticas recomendada al crear funciones de Azure.

- [Guía para desarrolladores de Azure Functions](functions-reference.md): contiene las referencias del programador para codificar las funciones y definir los desencadenadores y los enlaces.

- [Prueba de Azure Functions](functions-test-a-function.md): se describen las diversas herramientas y técnicas para probar sus funciones.