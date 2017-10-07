---
title: "Azure Active Directory B2C: uso de la personalización de idioma | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C: uso de la personalización de idioma

>[!NOTE] 
>Esta característica está en versión preliminar pública.  Se recomienda usar un inquilino de prueba cuando se utilice esta característica.  No planeamos nada en los últimos cambios de versión de disponibilidad general de toohello de vista previa de hello, pero nos reservamos toomake derecho Hola de esas características cambios tooimprove Hola.  Una vez que haya tenido una característica de tootry posibilidad, proporcionar comentarios sobre su experiencia y cómo podemos hacerlo mejor.  Puede proporcionar comentarios a través del portal de Azure Hola con la herramienta de cara sonriente de hello en la parte superior de hello derecho.   Si hay un requisito empresarial para toogo en directo con esta característica durante la fase de vista previa de hello, hacernos saber los escenarios y se podemos proporcionarle ayuda y orientación correcta de Hola.  Puede ponerse en contacto con nosotros en [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).

Personalización de idioma permite toochange su usuario viaje tooa otro idioma toosuit su cliente necesita.  Proporcionamos traducciones en 36 idiomas (vea [Información adicional](#additional-information)).  Incluso si su experiencia solo se proporciona para un único idioma, puede personalizar cualquier texto en hello páginas toosuit sus necesidades.  

## <a name="how-does-language-customization-work"></a>¿Cómo funciona la personalización de idioma?
Personalización de idioma permite tooselect qué idiomas su viaje de usuario está disponible en.  Una vez habilitada la característica de hello, puede proporcionar el parámetro de cadena de consulta de hello, ui_locales, desde la aplicación.  Cuando se llama a en Azure AD B2C, se traduce la configuración regional de toohello de página que ha indicado.  Utilizando el tipo de configuración proporciona un control total con respecto a los lenguajes de hello en su viaje de usuario y omite la configuración de idioma de hello del explorador del cliente de Hola. Como alternativa, quizás no necesite ese nivel de control sobre los idiomas que ve el cliente.  Si no proporciona un parámetro ui_locales, experiencia del cliente de hello viene determinada por la configuración de su explorador.  Todavía puede controlar qué idiomas es su viaje usuario traducen tooby agregarlo como un lenguaje compatible.  Si el explorador del cliente es tooshow de conjunto de un idioma no desea toosupport y, a continuación, idioma Hola seleccionado como valor predeterminado de referencias culturales admitidas se muestra en su lugar.

1. **las configuraciones regionales de interfaz de usuario especificado idioma** -una vez que habilita la personalización de idioma, el viaje de usuario es idioma traducido toohello aquí especificado
2. **Explorador solicitado lenguaje** -si se ha especificado ninguna interfaz de usuario y configuraciones regionales, traduce toohello explorador solicitado lenguaje, **si se ha incluido en los idiomas compatibles**
3. **Idioma predeterminado de directiva** -si explorador hello no especifica un idioma o especifica que no se admite, traduce idioma predeterminado de directiva de toohello

>[!NOTE]
>Si usa atributos de usuario personalizada, deberá tooprovide sus propias traducciones. Consulte "[Personalización de las cadenas](#customize-your-strings)" para más información.
>

## <a name="support-uilocales-requested-languages"></a>Compatibilidad con idiomas solicitados de ui_locales 
Habilitando "personalización de lenguaje' en una directiva, ahora puede controlar lenguaje Hola de viaje de usuario de hello agregando hello ui_locales parámetro.
1. [Siga estos hoja pasos toonavigate toohello B2C características Hola portal de Azure.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. Navegue directiva tooa que quiere tooenable de traducciones.
3. Haga clic en **Personalización de idioma**.
4. Leer Hola advertencia cuidadosamente.  Una vez habilitada, no puede desactivar la personalización de idioma.
5. Activar la característica de Hola y haga clic en **Aceptar**.
6. Guardar la directiva en hello superior izquierda de su **Editar directiva** hoja.

## <a name="select-which-languages-your-user-journey-supports"></a>Selección de los idiomas que admite el recorrido de usuario 
Crear una lista de idiomas permitidos para el toobe de viaje usuario traducido a cuando no se proporciona el parámetro de ui_locales Hola.
1. Asegúrese de que la directiva tenga habilitada la personalización de idioma según las instrucciones anteriores.
2. En la hoja **Editar directiva**, seleccione **Personalización de idioma**.
3. Se toman tooyour **idiomas admitidos** hoja.  Desde aquí, puede seleccionar **Agregar idioma**.
4. Seleccione todos los idiomas de Hola que le gustaría toobe compatible.  

>[!NOTE]
>Si no se proporciona un parámetro ui_locales, a continuación, Hola página es idioma del explorador del cliente toohello traducidos solo si está en esta lista
>

5. Haga clic en **Aceptar** final Hola
6. Hola cerrar **personalización de lenguaje** hoja y **guardar** la directiva.

## <a name="customize-your-strings"></a>Personalización de las cadenas
'Personalización de lenguaje' permite toocustomize cualquier cadena en su viaje de usuario.
1. Asegúrese de que la directiva tiene 'Lenguaje personalización' Habilitar desde instrucciones anteriores Hola.
2. En la hoja **Editar directiva**, seleccione **Personalización de idioma**.
3. En el menú de navegación izquierdo de hello, seleccione **descargar contenido**.
4. Seleccione página de Hola que desee tooedit.
5. En la lista desplegable de hello, seleccione el idioma de hello para que desea tooedit.
6. Haga clic en **Descargar**. 

Estos pasos proporcionan un archivo JSON que puede usar toostart editar las cadenas.

### <a name="changing-any-string-on-hello-page"></a>Cambiar cualquier cadena en la página de Hola
1. Hola abrir archivo JSON se descarga desde instrucciones anteriores en un editor de JSON.
2. Elemento de Hola de búsqueda que desea toochange.  Puede encontrar Hola `StringId` de cadena de hello está buscando, o busque hello `Value` desea toochange.
3. Hola de actualización `Value` atributo con el que desea mostrar.
4. Guarde el archivo hello y cargar los cambios.

### <a name="changing-extension-attributes"></a>Cambio de los atributos de extensión
Si está buscando cadena de hello toochange un atributo de usuario personalizada, o desea tooadd una toohello JSON, estará en hello siguiendo el formato:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Si necesita toooverride una cadena, que seguro Hola de tooset `Override` valor demasiado`true`.  Si no se cambia el valor de hello, se omite la entrada de Hola. 
>

Reemplace `<ExtensionAttribute>` con el nombre de Hola de su atributo de usuario personalizada.  
Reemplace `<ExtensionAttributeValue>` con hello nueva cadena toobe muestra.

### <a name="using-localizedcollections"></a>Uso de LocalizedCollections
Si desea tooprovide una lista de conjunto de valores para las respuestas, necesita toocreate un `LocalizedCollections`.  `LocalizedCollections` es una matriz de pares de `Name` y `Value`.  Hola `Name` es lo que se muestra y Hola `Value` es lo que se devuelve en la notificación de Hola.  tooadd una `LocalizedCollections`, tiene Hola siguiendo el formato:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Si necesita toooverride una cadena, que seguro Hola de tooset `Override` valor demasiado`true`.  Si no se cambia el valor de hello, se omite la entrada de Hola. 
>

* `ElementId`se hello usuario atributo que este `LocalizedCollections` es una respuesta a
* `Name`es usuario de toohello se muestra de Hola valor
* `Value`es lo que se devuelve en hello notificación cuando se selecciona esta opción

### <a name="upload-your-changes"></a>Carga de los cambios
1. Una vez haya completado el archivo JSON de hello cambios tooyour, navegue a tooyour atrás B2C inquilino.
2. En la hoja **Editar directiva**, seleccione **Personalización de idioma**.
3. En el menú de navegación izquierdo de hello, seleccione **cargar contenido**.
4. Seleccione página de hello que desea tooupload los cambios correspondientes.
5. Si desea tooupload un lenguaje que previamente ha proporcionado una JSON para, necesita toodelete Hola anterior entrada.  Puede eliminar, haga clic en hello `...` en Hola derecha de dicho lenguaje y seleccione **eliminar**.
6. Haga clic en **agregar** en la parte superior izquierda de Hola.
7. Seleccione el idioma de hello del archivo JSON.
8. Haga clic en botón de carpeta de hello en hello derecho y busque el archivo JSON.
9. Haga clic en hello **cargar** botón en la parte inferior de Hola de hoja de Hola.
10. Volver atrás tooyour **Editar directiva** hoja y haga clic en **guardar**.

## <a name="additional-information"></a>Información adicional
### <a name="recommendations-for-language-customization"></a>Recomendaciones para la personalización de idioma
Se recomienda solamente ponerles en recursos de idioma de tooyour entradas para las cadenas explícitamente desee tooreplace.  Se aplica un archivo de toohello de límite de tamaño que se compila fuera de las traducciones de JSON.  Si los archivos aumenten demasiados, afecta al rendimiento de Hola de su viaje de usuario.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>Las etiquetas de personalización de la IU de página se quitan una vez habilitada la personalización de idioma
Cuando se habilita la personalización de idioma, las ediciones anteriores de etiquetas que usan la personalización de IU de página se quitan, excepto para los atributos de usuario personalizados.  Este cambio se realiza tooavoid conflictos en donde puede editar las cadenas.  Puede seguir toochange las etiquetas y otras cadenas mediante la carga de recursos de idioma en 'Personalización de lenguaje'.
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Microsoft está confirmada tooprovide hello las traducciones más actualizadas para su uso
Mejoraremos continuamente las traducciones y garantizaremos su cumplimiento.  Agregaremos información identificar los cambios en la terminología global y errores y realizar actualizaciones de Hola que funcionarán sin problemas en su viaje de usuario.
### <a name="support-for-right-to-left-languages"></a>Compatibilidad con idiomas que se leen de derecha a izquierda
No hay compatibilidad con los idiomas que se leen de derecha a izquierda. Si necesita esta característica, vótela en [Comentarios de Azure](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).
### <a name="social-identity-provider-translations"></a>Traducciones de proveedores de identidades sociales
Proporcionamos hello ui_locales inicios de sesión OIDC parámetro toosocial pero no se cumple con algunos proveedores de identidades sociales, incluidas Facebook y Google. 
### <a name="browser-behavior"></a>Comportamiento del explorador
Chrome y Firefox ambos solicitar para su idioma de conjunto y si es un lenguaje compatible, se muestra antes de forma predeterminada Hola.  Borde actualmente no solicita un lenguaje y pasa el idioma predeterminado de toohello rectas.
### <a name="known-issues"></a>Problemas conocidos
* Cargar recursos de idioma para la página MFA de hello en una directiva de edición de perfil no está disponible actualmente.
* `LocalizedCollections`no se generan para los valores cuando sea necesario por tipo de respuesta de Hola
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>¿Y si quiero un idioma que no se admite?
Tenemos previsto tooprovide una extensión de esta característica que le permite tooupload un recurso JSON hacia 'idiomas personalizadas'.  característica de Hello permite toospecify nombre de Hola y lenguaje de código para ningún idioma y proporcionar *todos los* Hola traducciones para dicho idioma.  Si necesita esta característica, envíenos su escenario a [ aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).  

### <a name="what-languages-are-supported"></a>¿Qué idiomas se admiten?

| language              | Código de idioma |
|-----------------------|---------------|
| Bangla                | bn            |
| Checo                 | cs            |
| Danés                | da            |
| Alemán                | de            |
| Griego                 | el            |
| English               | en            |
| Español               | es            |
| Finés               | fi            |
| Francés                | fr            |
| Gujarati              | gu            |
| Hindi                 | hi            |
| Croata              | hr            |
| Húngaro             | hu            |
| Italiano               | it            |
| Japonés              | ja            |
| Kannada               | kn            |
| Coreano                | ko            |
| Malayalam             | ml            |
| Marathi               | mr            |
| Malayo                 | ms            |
| Noruego Bokmal      | nb            |
| Neerlandés                 | nl            |
| Punjabi               | pa            |
| Polaco                | pl            |
| Portugués (Brasil)   | pt-br         |
| Portugués (Portugal) | pt-pt         |
| Rumano              | ro            |
| Ruso               | ru            |
| Eslovaco                | sk            |
| Sueco               | sv            |
| Tamil                 | ta            |
| Telugu                | te            |
| Tailandés                  | th            |
| Turco               | tr            |
| Chino (simplificado)  | zh-hans       |
| Chino (tradicional) | zh-hant       |
