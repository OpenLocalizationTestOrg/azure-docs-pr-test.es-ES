---
title: "marcas de inicio de sesión en tooyour y páginas de Panel de acceso de la empresa de aaaAdd"
description: "Obtenga información acerca de cómo los hello y tooadd una página de toohello inicio de sesión Azure de personalización de marca de empresa acceder a la página del panel"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>Agregar marcas tooyour inicio de sesión y páginas de Panel de acceso de empresa
tooavoid confusión, muchas compañías desean tooapply una apariencia coherente en todos los sitios Web de Hola y servicios que administran. Azure Active Directory ofrece esta funcionalidad permitiéndole apariencia de hello toocustomize de hello después de páginas web con el logotipo de la compañía y combinaciones de colores personalizadas:

* **Página de inicio de sesión** : se trata de página de Hola que aparece al iniciar sesión en tooOffice 365 u otras aplicaciones basadas en web que usan Azure AD como proveedor de identidades. Interactuar con esta página durante una detección del dominio de inicio o tooenter sus credenciales. Hola Home Realm Discovery permite STS Hola sistema tooredirect federado usuarios tootheir local (por ejemplo, AD FS).
* **Página del Panel de acceso** : Hola Panel de acceso es un portal basado en web que permite tooview e iniciar Hola basada en la nube aplicaciones su administrador de Azure AD le concedió acceso a. tooaccess Hola Panel de acceso, Hola de uso después de la dirección URL: [https://myapps.microsoft.com](https://myapps.microsoft.com).

Este tema explica cómo puede personalizar la página de inicio de sesión de Hola y página del panel de acceso de Hola.

> [!NOTE]
> * Marcas de empresa es una característica que solo está disponible si ha actualizado toohello Premium o edición básica de Azure Active Directory, o un usuario de Office 365. Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md).
> * Azure Active Directory Premium y básicas ediciones están disponibles para los clientes de China mediante Hola instancia internacional de Azure Active Directory. Azure Active Directory Premium y las ediciones básicas no se admiten actualmente en el servicio de Microsoft Azure Hola operado por 21Vianet en China. Para obtener más información, póngase en contacto con nosotros en hello [foro de Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).
>
>

## <a name="customizing-hello-sign-in-page"></a>Personalizar la página de inicio de sesión de Hola
Por lo general, si tiene aplicaciones de acceso basado en explorador tooyour en la nube y los servicios que su organización se suscribe a, utilice página de inicio de sesión de Hola.

Si ha aplicado la página de inicio de sesión de tooyour de cambios, puede tardar una hora tooan Hola cambios tooappear.

Las páginas de inicio de sesión con marca solamente aparecen cuando se visita un servicio con una dirección URL específica del inquilino, como https://outlook.com/**contoso**.com o https://mail.**contoso**.com.

Si visita un servicio con direcciones URL que no son específicas de un inquilino (por ejemplo, https://mail.office365.com), aparece una página de inicio de sesión sin marca. En este caso, la marca solamente aparecerá una vez que haya especificado el identificador de usuario o haya seleccionado un icono de usuario.

> [!NOTE]
> * El nombre de dominio debe aparecer como "Activo" Hola **Active Directory** > **directorio** > **dominios** sección de hello portal de Azure clásico donde se ha configurado la marca.
> * Personalización de la página de inicio de sesión no dirige toohello consumidor inicio de sesión en la página de Microsoft. Si inicia sesión con una cuenta Microsoft personal, puede ver una lista con marca de mosaicos de los usuarios presentada por Azure AD, pero Hola la marca de su organización no aplicará toohello página de inicio de sesión de cuenta de Microsoft.
>
>

Si desea que tooshow su marca de empresa, colores y otros elementos personalizables en esta página, vea Hola después imágenes toounderstand Hola diferenciar dos experiencias de Hola.

Hola siguiente captura de pantalla muestra y ejemplo de página de inicio de sesión de hello Office 365 en un equipo de escritorio **antes de** una personalización:

![Página de inicio de sesión de Office 365 antes de la personalización][1]

Hola siguiente captura de pantalla muestra y ejemplo de página de inicio de sesión de hello Office 365 en un equipo de escritorio **después** una personalización:

![Página de inicio de sesión de Office 365 después de la personalización][2]

Hello captura de pantalla siguiente muestra un ejemplo de página de inicio de sesión de hello Office 365 en un dispositivo móvil **antes de** una personalización:

![Página de inicio de sesión de Office 365 antes de la personalización][3]

Hello captura de pantalla siguiente muestra un ejemplo de página de inicio de sesión de hello Office 365 en un dispositivo móvil **después** una personalización:

![Página de inicio de sesión de Office 365 después de la personalización][4]

Cuando cambia el tamaño de una ventana del explorador, Hola ilustración grande, como Hola mostrado anteriormente, se recorta a menudo tooaccommodate relaciones de aspecto de pantalla diferentes. Teniendo esto en cuenta, debe intentar elementos visuales de tookeep Hola clave en la ilustración de Hola para que siempre aparecen en la esquina superior izquierda de hello (parte superior derecha para idiomas de derecha a izquierda). Esto es importante porque el redimensionamiento normalmente se produce en curso de la esquina inferior derecha de hello hacia Hola superior o izquierdo o desde la parte inferior de hello hacia la parte superior de Hola.

Hello siguiente imagen muestra cómo se recorta ilustración hello cuando el Explorador de hello es cuyo tamaño ha cambiado toohello izquierda:

![][6]

Aquí es cómo aparece después de hello explorador se redimensiona hacia la parte superior de hello:

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>¿Qué elementos de la página de hello puedo personalizar?
Puede personalizar Hola siguientes elementos en la página de inicio de sesión de hello:

![][5]

| Elemento de la página | Ubicación en la página de Hola |
|:--- | --- |
| Logotipo del banner |Se muestra en hello superior derecha de la página de Hola. Reemplaza el sitio de destino de Hola Hola logotipo que va a iniciar sesión en toodisplays (por ejemplo Office 365 o Azure). |
| Ilustración grande / Color de fondo |Se muestra a la izquierda de Hola de página Hola. Reemplaza el sitio de destino de Hola Hola imagen que va a iniciar sesión en toodisplays. Hola Color de fondo puede se muestre en lugar de hello ilustración grande en conexiones de ancho de banda bajo o en pantallas estrechas. |
| Mantener la sesión iniciada |Se muestra en el cuadro de texto de contraseña de Hola. |
| Texto de la página de inicio de sesión |Se muestra por encima del pie de página de hello cuando necesite tooconvey información útil antes de un inicio de sesión de con una cuenta profesional o educativa. Por ejemplo, puede que desee tooinclude Hola teléfono número tooyour asistencia o una declaración legal. |

> [!NOTE]
> Todos los elementos son opcionales. Por ejemplo, si se especifica un logotipo de Banner pero no una ilustración grande, página de inicio de sesión de hello muestra la ilustración hello y logotipo de sitio de destino de hello (es decir, imagen de autopista de hello Office 365 California).
>
>

En la página de inicio de sesión, Hola **mantener la sesión iniciada** casilla permite un tooremain usuario inicie sesión cuando cierre y vuelva a abre su explorador. No afecta a la duración de la sesión. Puede ocultar Hola casilla en la página de inicio de sesión de Azure Active Directory de Hola.

Si se muestra la casilla de verificación de hello depende de la configuración de Hola de **KMSI ocultar**.

![][9]

toohide Hola casilla, configure esta opción demasiado**Hidden**.

> [!NOTE]
> Algunas características de SharePoint Online y Office 2010 dependen de los usuarios que están toocheck capaz de este cuadro. Si configura esta toohidden de configuración, los usuarios pueden ver mensajes adicionales e inesperadas en toosign.
>
>

También puede localizar todos los elementos de esta página. Una vez que haya configurado un conjunto de elementos de personalización "predeterminado", puede configurar más versiones para las diferentes configuraciones regionales. También puede mezclar y hacer coincidir varios elementos. Por ejemplo, puede:

* Crear una ilustración grande "predeterminada" que funcione para todas las culturas y, a continuación, crear versiones específicas para inglés y francés. Cuando se establece su tooone de exploradores de estos dos idiomas, aparece imagen específica de hello, mientras ilustración de hello predeterminada aparece para todos los demás lenguajes.
* Configure logotipos diferentes para su organización (por ejemplo, para las versiones en japonés o hebreo).

## <a name="access-panel-page-customization"></a>Personalización de la página del panel de acceso
página de Panel de acceso de Hello es básicamente una página de portal para aplicaciones de nube de acceso rápido toohello que le ha concedido acceso a tooby el administrador. En esta página, las aplicaciones aparecen como iconos de aplicaciones interactivas.

Hola siguiente captura de pantalla muestra un ejemplo de una página de panel de acceso después de la personalización.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>Configuración de su directorio con la información de marca de empresa
Puede configurar un conjunto predeterminado de elementos personalizables por directorio en hello portal de Azure clásico. Una vez que se guardaron los valores predeterminados de hello, un administrador puede agregar versiones localizadas de cada elemento, para los distintos idiomas y configuraciones regionales. Todos los elementos personalizables son opcionales.

Por ejemplo, si configura un logotipo de Banner predeterminado pero no una ilustración grande, página de inicio de sesión de hello muestra su logotipo en la esquina superior derecha de Hola. Sin embargo, se muestra la ilustración de hello predeterminada del sitio de Hola.

Imagine Hola siguiente configuración:

* Un logotipo del banner predeterminado y el inicio de sesión en el texto de página en inglés
* Un texto de la página de inicio de sesión específico para un idioma en alemán

Si la preferencia de idioma es alemán, obtendrá Hola predeterminado logotipo del Banner pero Hola texto en alemán.

Aunque técnicamente podría configurar un conjunto diferente para cada idioma admitido por Azure AD, se recomienda que mantenga número Hola de variantes baja, por motivos de mantenimiento y rendimiento.

> [!IMPORTANT]
> Yammer no no mostrar hello Azure AD con la marca de página de inicio de sesión hasta después de hello usuario inicia sesión. usuario de Hello ve Hola genérica página de inicio de sesión en Office 365 en primer lugar y, a continuación, Hola marca página después de eso.   
 
 
**tooadd personalización de marca de tooyour de directorio de la compañía, lleve a cabo Hola pasos:**

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador del directorio de hello desea toocustomize.
2. Seleccione el directorio de hello desea toocustomize.
3. En la barra de herramientas de hello en la parte superior de hello, haga clic en **configurar**.
4. Haga clic en **Personalizar la información de marca**.
5. Modificar elementos de hello desea toocustomize. Todos los campos son opcionales.
6. Haga clic en **Guardar**.

Puede tardar hasta hora tooan nuevo cambio se realiza toohello inicio de sesión página de personalización de marca tooappear.

**organización de específica del lenguaje de tooadd personalización de marca, llevar a cabo Hola pasos:**

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador del directorio de hello desea toocustomize.
2. Seleccione el directorio de hello desea toocustomize.
fs3. En la barra de herramientas de hello en la parte superior de hello, haga clic en **configurar**.
4. Haga clic en **Personalizar la información de marca**.
5. Haga clic en **Agregar personalización de marca para un idioma específico**.
6. Seleccionar idioma de Hola que desee toocustomize logotipo de Hola para y, a continuación, haga clic en **siguiente**.
7. Edite únicamente los elementos de hello para el que desea que invalida tooconfigure específica del lenguaje. Todos los campos son opcionales. Si un campo se deja en blanco, a continuación, Hola personalizada predeterminada valor se muestra en su lugar (u Hola predeterminada de Microsoft si no se ha configurado un valor predeterminado personalizado).
8. Haga clic en **Guardar**.

**tooremove marcas de empresa de su directorio, realizar Hola pasos:**

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) como administrador del directorio de hello desea toocustomize.
2. Seleccione el directorio de hello desea toocustomize.
3. En la barra de herramientas de hello en la parte superior de hello, haga clic en **configurar**.
4. Haga clic en **Personalizar la información de marca**.
5. En la página Personalizar marca hello, seleccione **Editar configuración de personalización de marca existente** y, a continuación, ir a página siguiente de toohello.
6. Dependiendo de qué elementos desea tooremove, siga uno o varios de los siguientes hello:

    a. En **Logotipo del banner**, seleccione **Quitar logotipo cargado** .

    b. En **Logotipo de imagen**, seleccione **Quitar logotipo cargado**.

    c. Quite el texto hello de todos los cuadros de texto.

    d. Haga clic en **Next**.

    e. Quite el texto hello de todos los cuadros de texto.
7. Haga clic en **guardar** elementos de hello tooremove.
8. Si es necesario, haga clic en **personalizar marca** nuevo y repita estos pasos para quita todos los específicos del idioma personalización de marca que necesita toobe.
    Se quitaron todas las opciones de personalización de marca al hacer clic en **personalizar marca** y vea hello **personalizar información de marca predeterminada** formulario sin ajustes existentes configurados.

## <a name="testing-and-examples"></a>Pruebas y ejemplos
Se recomienda que experimente con un inquilino de prueba antes de realizar cambios en el entorno de producción.

**tooverify si su marca se ha aplicado:**

1. Abra una sesión de explorador InPrivate o de incógnito.
2. Visite https://outlook.com/contoso.com, sustituir contoso.com por dominio de Hola que ha personalizado.

Esto también funciona con los dominios que tengan un aspecto similar a contoso.onmicrosoft.com.

toohelp crear conjuntos de personalización efectivos, hemos personalizado Hola después de dos páginas de inicio de sesión ficticias:

* [http://AKA.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://AKA.ms/aaddemo002](http://aka.ms/aaddemo002)

configuración específica del idioma de tootest hello, necesita las preferencias de idioma de toomodify Hola predeterminado en el idioma de tooa del explorador web que ha establecido en la personalización. En Internet Explorer, puede configurar esto en hello **opciones de Internet** menú.

## <a name="customizable-elements"></a>Elementos personalizables
Algunos elementos personalizables de Azure AD disponen de múltiples casos de uso. Puede configurar los logotipos de empresa una vez por cada directorio y se utiliza en ambos, en el inicio de sesión de Hola y páginas de Panel de acceso. Algunos elementos personalizables son solo toohello inicio de sesión página específica. Hello tabla siguiente proporciona detalles para hello diferentes elementos personalizables.

| Nombre | Description | Restricciones | Recomendaciones |
| --- | --- | --- | --- |
| Logotipo del banner |Hola logotipo del Banner se muestra en la página de inicio de sesión de Hola y panel de acceso de Hola. |<p>JPG o PNG</p><p>60x280 píxeles</p><p>10 kB</p> |<p>Utilice el logotipo completo de la organización (incluido el pictograma y el logotipo).</p><p>Mantener ocupe más de 30 píxeles tooavoid alta Introducción a las barras de desplazamiento en dispositivos móviles</p><p>Manténgalo por debajo de 4 kB.</p><p>Utilice un PNG transparente (no presuponga esa página de inicio de sesión de hello siempre tiene un fondo blanco)</p> |
| Logotipo del icono |(actualmente si no se han utilizado en la página de inicio de sesión de hello) Hola futuro, este texto puede ser usado tooreplace Hola genérico "cuenta profesional o educativa" pictograma en diferentes lugares de la experiencia de Hola. |<p>JPG o PNG</p><p>120x120 píxeles</p><p>10 kB</p> |<p>Mantenerlo simple (sin texto pequeño), esta imagen puede ser too50 cuyo tamaño ha cambiado % |
| </p> | | | |
| Etiqueta de nombre de usuario de la página de inicio de sesión |(actualmente si no se han utilizado en la página de inicio de sesión de hello) Hola futuro, este texto puede ser usado tooreplace Hola cadena genérica "cuenta profesional o educativa" en diferentes lugares de la experiencia de Hola. Puede establecer toosomething como "Cuenta Contoso" o "Id. de Contoso." |<p>Texto Unicode, los caracteres de too50</p><p>Solo texto sin formato (sin vínculos ni etiquetas HTML)</p> |<p>Elija una etiqueta corta y sencilla.</p><p>Pida a los usuarios cómo se suelen referir trabajo toohello o cuenta organizativa que les proporcionó.</p> |
| Texto de la página de inicio de sesión |Este texto "reutilizable" aparece debajo de formulario de la página de inicio de sesión de Hola y puede ser usado toocommunicate más instrucciones, o donde tooget ayuda y soporte técnico. |<p>Texto Unicode, los caracteres de too256</p><p>Solo texto sin formato (sin vínculos ni etiquetas HTML)</p> |No sobrepase los 250 caracteres (aproximadamente 3 líneas de texto) |
| Ilustración de la página de inicio de sesión |ilustración de Hello es una imagen grande que se muestra en hello inicio de sesión página toohello a la izquierda del formulario de la página de inicio de sesión de Hola. |<p>JPG o PNG</p><p>1420x1200</p><p>500 kB</p> |<p>1420x1200 píxeles</p><p>Importante: manténgala lo más pequeña posible, lo ideal es que no sobrepase los 200 KB. Si esta imagen es demasiado grande, rendimiento de Hola de página de inicio de sesión de Hola se ve afectado cuando no está en la caché de imagen de Hola</p><p>Esta imagen a menudo se recorta, tooaccommodate diferentes relaciones de pantalla. Mantener elementos visuales principales de hello en hello esquina superior izquierda (esquina superior derecha para idiomas de derecha a izquierda), ya que el cambio de tamaño se produce desde la esquina inferior/derecha hello, va hacia Hola superior o izquierdo, tal y como se reduce la ventana del explorador Hola.</p> |
| Color de fondo de la página de inicio de sesión |color de fondo de página de inicio de sesión de Hola se usa en la izquierda de toohello Hola área de formulario de la página de inicio de sesión de Hola. |Debe ser un color RGB en formato hexadecimal (ejemplo: #FFFFFF) |<p>color de fondo de Hola que se muestre en lugar de hello ilustración grande en conexiones de ancho de banda bajo</p><p>Se recomienda seleccionar color principal Hola Hola logotipo del Banner</p> |

## <a name="next-steps"></a>Pasos siguientes
* [Introducción a Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
