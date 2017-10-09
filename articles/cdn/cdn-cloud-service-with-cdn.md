---
title: aaaIntegrate un servicio de nube de Azure con red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy un servicio de nube sirve contenido desde un punto de conexión de red CDN de Azure integrada"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a> Integración de un servicio en la nube con la Red de entrega de contenido (CDN) de Azure
Un servicio de nube puede integrarse con CDN de Azure, que sirve al contenido de la ubicación del servicio de nube de Hola. Esto deja de enfoque Hola siguientes ventajas:

* Fácil implementación y actualización de imágenes, scripts y hojas de estilo en los directorios de proyecto del servicio en la nube
* Actualizar fácilmente los paquetes de NuGet de hello en el servicio de nube, por ejemplo, jQuery o versiones de arranque
* Administrar la aplicación Web y la red CDN en ser atendido contenido todas de hello misma interfaz de Visual Studio
* Flujo de trabajo de implementación unificado para la aplicación web y el contenido servido por CDN
* Integración de unión y minificación de ASP.NET con CDN de Azure

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este tutorial, aprenderá a:

* [Integración de un extremo de red CDN de Azure con el servicio en la nube y suministro de contenido estático en las páginas web desde CDN de Azure](#deploy)
* [Configuración de los valores de la caché para el contenido estático en el servicio en la nube](#caching)
* [Suministro de contenido de acciones de controlador a través de la red CDN de Azure](#controller)
* [Servir empaquetan y reduce el contenido a través de la red CDN de Azure conservando la experiencia en Visual Studio de depuración de script de Hola](#bundling)
* [Configuración de la reserva de los scripts y CSS cuando la red CDN de Azure está sin conexión](#fallback)

## <a name="what-you-will-build"></a>Lo que va a crear
Implementar un rol de Web de servicio de nube mediante predeterminado Hola plantilla de ASP.NET MVC, agregará contenido de tooserve de código de una CDN de Azure integrada, como una imagen, los resultados de acción de controlador y archivos de JavaScript y CSS de predeterminados hello y también escribir hello tooconfigure de código mecanismo de reserva para agrupaciones atendido en caso de hello ese CDN Hola está sin conexión.

## <a name="what-you-will-need"></a>Qué necesita
Este tutorial tiene Hola siguiendo los requisitos previos:

* Una [cuenta de Microsoft Azure activa](/account/)
* Visual Studio 2015 con el [SDK de Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Necesita una cuenta de Azure toocomplete este tutorial:
> 
> * También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/) -obtendrá créditos puede usar tootry los servicios de Azure de pago e incluso después de que se utilizan hasta puede mantener la cuenta de hello y libre de usar servicios de Azure, como sitios Web.
> * Puede [activar las ventajas de suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Su suscripción a MSDN le proporciona crédito todos los meses que puede utilizar para servicios de Azure de pago.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>un servicio en la nube
En esta sección, se implementar predeterminado Hola plantilla de aplicación de ASP.NET MVC en Visual Studio 2015 tooa rol de Web de servicio de nube y, a continuación, se integre con un nuevo extremo de red CDN. Siga estas instrucciones hello:

1. En Visual Studio 2015, crear un nuevo servicio de nube de Azure desde la barra de menús de hello yendo demasiado**archivo > Nuevo > proyecto > nube > servicio de nube de Azure**. Asígnele un nombre y haga clic en **Aceptar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Seleccione **rol Web de ASP.NET** y haga clic en hello  **>**  botón. Haga clic en Aceptar.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Seleccione **MVC** y haga clic en **Aceptar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Ahora, publicar este tooan de rol Web servicio de nube de Azure. Haga clic en proyecto de servicio de nube de Hola y seleccione **publicar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Si todavía no se ha suscrito a Microsoft Azure, haga clic en hello **agregar una cuenta...**  Hola de lista desplegable y haga clic en **agregar una cuenta** elemento de menú.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. En la página de inicio de sesión hello, inicie sesión con hello cuenta de Microsoft que usó tooactivate su cuenta de Azure.
7. Una vez que haya iniciado la sesión, haga clic en **Siguiente**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Suponiendo que no haya creado un servicio en la nube o una cuenta de almacenamiento, Visual Studio le ayudará a crear ambos. Hola **crear servicio en la nube y cuenta** cuadro de diálogo, nombre de servicio que desee de tipo hello y región deseada Hola select. A continuación, haga clic en **Crear**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. Hola, página de configuración de publicación, comprobar la configuración de Hola y haga clic en **publicar**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > proceso de publicación de Hola para servicios en la nube tarda mucho tiempo. Hola habilitar Web Deploy para la opción de todos los roles puede dificultar la depuración de servicio en la nube mucho más rápido proporcionando actualizaciones rápido (aunque temporal) tooyour roles Web. Para obtener más información sobre esta opción, vea [publicar un servicio de nube mediante herramientas de Azure de hello](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Cuando Hola **Microsoft Azure Activity Log** muestra que el estado de publicación es **completado**, creará un punto de conexión de red CDN que se integra con este servicio de nube.
   
   > [!WARNING]
   > Si, después de publicarlo, servicio de nube de hello implementado muestra una pantalla de error, es probable porque está usando el servicio de nube de Hola que ha implementado un [invitado SO que no incluye .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  Puede solucionar este problema mediante la [implementación de .NET 4.5.2 como tarea de inicio](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Crear un nuevo perfil de CDN
Un perfil de red de entrega de contenido es una colección de puntos de conexión de red de entrega de contenido.  Cada perfil contiene uno o más de estos puntos de conexión de CDN.  Puede ser conveniente toouse varios tooorganize perfiles los extremos de red CDN el dominio de internet, las aplicaciones web u otros criterios.

> [!TIP]
> Si ya tiene un perfil de CDN que desea toouse para este tutorial, continúe demasiado[crear un nuevo extremo CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Crear un nuevo extremo de CDN
**toocreate un nuevo extremo de red CDN para la cuenta de almacenamiento**

1. Hola [Portal de administración de Azure](https://portal.azure.com), navegar por el perfil de CDN tooyour.  Puede haber anclarlo toohello panel en el paso anterior de Hola.  Si no es así, se encontrará, haciendo clic en **examinar**, a continuación, **perfiles de red CDN**, y haga clic en el perfil de hello tiene previsto tooadd del extremo que.
   
    aparece la hoja de perfil CDN Hola.
   
    ![Perfil de CDN][cdn-profile-settings]
2. Haga clic en hello **Agregar extremo** botón.
   
    ![Botón Agregar punto de conexión][cdn-new-endpoint-button]
   
    Hola **agregar un punto de conexión** aparece hoja.
   
    ![Hoja Agregar punto de conexión][cdn-add-endpoint]
3. Escriba un **Nombre** para este punto de conexión de red de entrega de contenido.  Este nombre será tooaccess usa los recursos almacenados en caché en el dominio de hello `<EndpointName>.azureedge.net`.
4. Hola **tipo de origen** lista desplegable, seleccione *servicio en la nube*.  
5. Hola **nombre de host de origen** de lista desplegable, seleccione el servicio de nube.
6. Deje los valores predeterminados de Hola para **ruta de acceso de origen**, **encabezado de host de origen**, y **puerto de protocolo/origen**.  Debe especificar al menos un protocolo (HTTP o HTTPS).
7. Haga clic en hello **agregar** toocreate botón Hola nuevo punto de conexión.
8. Una vez que se crea el extremo de hello, aparece en una lista de puntos de conexión para el perfil de Hola. vista de lista de Hello muestra hello URL toouse tooaccess almacenado en memoria caché de contenido, así como dominio de origen de Hola.
   
    ![Punto de conexión de CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > punto de conexión de Hello no inmediatamente estará disponible para su uso.  Puede tardar minutos too90 hello toopropagate de registro a través de la red CDN Hola. Los usuarios que intenten nombre de dominio de red CDN Hola de toouse inmediatamente pueden recibir el código de estado 404 hasta que esté disponible a través de la red CDN Hola contenido Hola.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Hola extremo de red CDN de prueba
Cuando es el estado de publicación de hello **completado**, abra una ventana del explorador y navegue demasiado**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. En nuestra instalación, esta URL es:

    http://camservice.azureedge.net/Content/bootstrap.css

Que corresponde a toohello después de la dirección URL de origen en el extremo de red CDN Hola:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

Cuando se desplaza demasiado**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, según el navegador, será toodownload solicitada o abrir hello bootstrap.css que que procede de la aplicación Web publicada.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

Puede acceder de forma parecida a cualquier dirección URL de acceso público en **http://*&lt;serviceName>*.cloudapp.net/** directamente desde el punto de conexión de la red CDN. Por ejemplo:

* Un archivo .js de ruta de acceso / script de Hola
* Cualquier archivo de contenido de Hola/Content ruta de acceso
* Cualquier controlador/acción
* Si la cadena de consulta de hello está habilitada en el punto de conexión de red CDN, cualquier dirección URL con cadenas de consulta

De hecho, con hello por encima de la configuración, puede hospedar un servicio nube todo Hola desde  **http://*&lt;cdnName >*.azureedge.net/**. Si desplaza demasiado**http://camservice.azureedge.net/ **, se pueden transferir el resultado de acción de Hola de Home/Index.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Esto no significa, sin embargo, que siempre es un tooserve buena idea un servicio de nube todo a través de la red CDN de Azure. 

Una CDN con la optimización de entrega estático no necesariamente acelerar la entrega de activos dinámicas que no están diseñadas toobe almacenado en memoria caché o se actualizan con mucha frecuencia, ya que la CDN Hola debe extraiga una nueva versión del recurso de Hola de servidor de origen de hello muy a menudo. En este escenario, puede habilitar [aceleración de sitio dinámico](cdn-dynamic-site-acceleration.md) optimización (DSA) en el punto de conexión que utiliza varios toospeed técnicas la entrega de activos dinámicos no almacenable en caché. 

Si tiene un sitio con una combinación de contenido estático y dinámico, puede elegir tooserve el contenido estático de CDN con un tipo de optimización estático (por ejemplo, entrega de web general) y contenido dinámico tooserve directamente desde el servidor de origen de Hola o a través de una CDN punto de conexión con la optimización de DSA activada caso por caso. toothat final, ya ha visto cómo los archivos de contenido individuales tooaccess desde el punto de conexión de red CDN Hola. Le mostrará cómo tooserve una acción de un controlador específico a través de un punto de conexión de red CDN concreto en servir contenido de las acciones de controlador a través de la red CDN de Azure.

alternativa de Hello es toodetermine qué contenido tooserve de red CDN de Azure de forma caso por caso en el servicio de nube. toothat final, ya ha visto cómo los archivos de contenido individuales tooaccess desde el punto de conexión de red CDN Hola. Le mostrará cómo tooserve una acción de un controlador específico a través de Hola extremo de red CDN en [servir el contenido de las acciones de controlador a través de la red CDN de Azure](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Configuración de las opciones de caché para los archivos estáticos del servicio en la nube
Con la integración de CDN de Azure en su servicio en la nube, puede especificar cómo desea estático toobe contenido en caché en el extremo de red CDN Hola. toodo, abra *Web.config* de su rol Web de proyecto (por ejemplo, WebRole1) y agregue un `<staticContent>` elemento demasiado`<system.webServer>`. Hola XML siguiente configura Hola caché tooexpire en 3 días.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

Una vez hecho esto, todos los archivos estáticos en el servicio de nube observará Hola igual de regla en la memoria caché de la red CDN. Para un control más granular de la configuración de la caché, agregue un archivo *Web.config* a una carpeta y agregue ahí su configuración. Por ejemplo, agregar un *Web.config* archivo toohello *\Content* carpeta y reemplazar Hola contenido con hello continuación de XML:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Esta configuración hace que todos los archivos estáticos de hello *\Content* toobe de carpeta en caché durante 15 días.

Para obtener más información acerca de cómo hello tooconfigure `<clientCache>` elemento, vea [memoria caché del cliente &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

En [servir el contenido de las acciones de controlador a través de la red CDN de Azure](#controller), también le mostrará cómo puede configurar configuración de caché de resultados de la acción de controlador en caché la red CDN Hola.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Suministro de contenido de acciones de controlador a través de la red CDN de Azure
Al integrar un rol Web de servicio de nube con la red CDN de Azure, es tooserve es relativamente fácil de contenido de las acciones de controlador a través de hello CDN de Azure. Aparte de servir la nube de servicio directamente a través de la red CDN de Azure (que se muestra anteriormente), [Maarten Balliauw](https://twitter.com/maartenballiauw) muestra cómo toodo con realizar un recorrido divertido MemeGenerator controlador [reducir la latencia en web Hola con hello CDN de Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). Aquí simplemente lo vamos a reproducir.

Imagine que en su servicio en la nube que desee memes toogenerate basada en una imagen de Chuck Norris jóvenes (fotografías por [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) similar a la siguiente:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

Tiene un sencillo `Index` acción que permite a los clientes de hello toospecify superlativas de hello en imagen de hello, a continuación, genera Hola personaje una vez que acción posterior a la toohello. Puesto que es Chuck Norris, se podría esperar este toobecome página bastante popular globalmente. Este es un buen ejemplo de servir contenido dinámico con CDN de Azure.

Siga pasos anteriores toosetup con hello esta acción de controlador:

1. Hola *\Controllers* carpeta, cree un archivo .cs denominado *MemeGeneratorController.cs* y reemplazar Hola contenido con hello siguiendo el código. Ser parte resaltada de hello tooreplace seguro con el nombre de red CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Pulse el botón derecho en el valor predeterminado de hello `Index()` acción y seleccione **agregar vista**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Acepte la configuración de Hola a continuación y haga clic en **agregar**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Hola abrir nueva *Views\MemeGenerator\Index.cshtml* y reemplazar el contenido de hello con hello sigue HTML simple para enviar superlativas hello:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Vuelva a publicar el servicio de nube de Hola y navegue demasiado**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** en el explorador.

Cuando se envían los valores del formulario Hola demasiado`/MemeGenerator/Index`, hello `Index_Post` método de acción devuelve un vínculo toohello `Show` método de acción con el identificador de entrada respectivos Hola. Al hacer clic en el vínculo de hello, alcanzar Hola siguiente código:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Si se asocia el depurador local, obtendrá experiencia de depuración normal de hello con una redirección local. Si se está ejecutando en el servicio de nube de hello, redirigirá al:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Que corresponde a toohello después de la dirección URL de origen en el punto de conexión:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


A continuación, puede usar hello `OutputCacheAttribute` atributo hello `Generate` toospecify método cómo debe almacenarse en caché el resultado de acción de hello, que respeta la CDN de Azure. código de Hello siguiente especifica una expiración de caché de 1 hora (3600 segundos).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Del mismo modo, puede servir el contenido de cualquier acción de controlador en el servicio de nube a través de la red CDN de Azure, con la opción de almacenamiento en caché de hello deseado.

En la siguiente sección hello, mostraré cómo tooserve Hola agrupadas y reduce las secuencias de comandos y CSS a través de la red CDN de Azure.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Integración de unión y minificación de ASP.NET con CDN de Azure
Hojas de estilos CSS y secuencias de comandos cambian con poca frecuencia y son los principales candidatos para la caché de Azure CDN Hola. Rol Web que se sirva Hola todo a través de la red CDN de Azure es toointegrate de manera más fácil de hello agrupación y minificación con CDN de Azure. Sin embargo, como puede que no desee toodo esto, le mostrará cómo toodo mientras conserva Hola había deseado Developer experiencia de ASP.NET agrupar y minificar, como:

* Gran experiencia en el modo de depuración
* Implementación optimizada
* Actualizaciones inmediatas tooclients para las actualizaciones de versión de secuencia de comandos/CSS
* Mecanismo de reserva cuando el extremo de red CDN falla
* Menor modificación del código

Hola **WebRole1** proyecto que creó en [integrar un punto de conexión de red CDN de Azure con su sitio Web de Azure y servir contenido estático en las páginas Web de la red CDN de Azure](#deploy), abra *App_Start\ BundleConfig.cs* y eche un vistazo a hello `bundles.Add()` llamadas al método.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

Hola primero `bundles.Add()` instrucción agrega una agrupación de scripts en el directorio virtual de hello `~/bundles/jquery`. A continuación, abra *Views\Shared\_Layout.cshtml* toosee cómo se representa la etiqueta de agrupación de script de Hola. Debe ser hello toofind pueda después de la línea de código Razor:

    @Scripts.Render("~/bundles/jquery")

Cuando se ejecuta este código Razor en función de hello Web de Azure, se representará un `<script>` etiqueta para hello script siguiente toohello similar de agrupación:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Sin embargo, cuando se ejecuta en Visual Studio escribiendo `F5`, representará individualmente cada archivo de script de agrupación de Hola (en caso de hello anterior, solo un archivo de scripts está en agrupación de hello):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Esto le permite toodebug código de JavaScript de hello en el entorno de desarrollo mientras lo que reduce las conexiones de cliente simultáneas (unión) y se mejora el archivo descargar rendimiento (minificación) en producción. Es un toopreserve característica excelente con la integración de CDN de Azure. Además, puesto que la agrupación de hello representa ya contiene una cadena de versión generada automáticamente, desea tooreplicate que funcionalidad Hola por lo que cada vez que actualice su versión de jQuery a través de NuGet, se puede actualizar en el cliente hello tan pronto como es posible.

Siga los pasos de Hola por debajo de la agrupación de ASP.NET de toointegration y minificación con el punto de conexión.

1. En *App_Start\BundleConfig.cs*, modificar hello `bundles.Add()` toouse métodos otra [constructor agrupación](http://msdn.microsoft.com/library/jj646464.aspx), que especifica una dirección de red CDN. toodo, Hola reemplazar `RegisterBundles` definición de método con el siguiente código de hello:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Ser seguro tooreplace `<yourCDNName>` con nombre hello la red CDN de Azure.
   
    En palabras sencillas, se establece `bundles.UseCdn = true` y agrega una agrupación de tooeach de dirección URL de CDN cuidadosamente diseñada. Por ejemplo, hello primer constructor en el código de hello:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    se Hola igual que:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Este constructor indica a ASP.NET agrupar y minificar toorender de archivos de script individuales cuando depura localmente, pero use Hola especificado CDN dirección tooaccess hello secuencia de comandos en cuestión. Sin embargo, observe dos características importantes con esta URL de red CDN diseñada especialmente:
   
   * origen de Hola para esta dirección URL de la red CDN es `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que es realmente Hola de directorio virtual de la agrupación de scripts de hello en el servicio de nube.
   * Puesto que utiliza el constructor de la red CDN, etiqueta de script CDN para agrupación Hola Hola ya no contiene cadena de versión de Hola generada automáticamente en hello representado la dirección URL. También debe generar manualmente una cadena de versión único cada vez que agrupación de scripts de Hola se tooforce modificado se pierda una memoria caché en la red CDN de Azure. Hola al mismo tiempo, esta cadena de versión único debe permanecer constante a través de la vida de Hola Hola implementación toomaximize de aciertos de caché en la red CDN de Azure después de implementa el paquete de saludo.
   * Hola de cadena de consulta v = < W.X.Y.Z > extracciones de *Properties\AssemblyInfo* en su proyecto de rol Web. Puede tener un flujo de trabajo de implementación que incluya incrementar la versión del ensamblado hello cada vez que publique tooAzure. O bien, simplemente puede modificar *Properties\AssemblyInfo* en la cadena de versión de proyecto tooautomatically incremento Hola cada vez que compile, utilizando el carácter comodín de hello ' *'. Por ejemplo:
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     Otro toostreamline de estrategia generando una cadena única para la vida de una implementación de hello funcionará aquí.
2. Volver a publicar Hola nube acceso y el servicio Hola página principal.
3. Hola de la vista código HTML de la página de Hola. Debe ser capaz de toosee Hola representan con una cadena de versión único cada vez que vuelve a publicar servicio en la nube tooyour cambios de dirección URL de CDN. Por ejemplo:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. En Visual Studio, depurar el servicio de nube de hello en Visual Studio escribiendo `F5`.,
5. Hola de la vista código HTML de la página de Hola. Aún verá cada archivo de script procesado de forma individual para que pueda tener una experiencia de depuración coherente en Visual Studio.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Mecanismo de reserva para URL de red CDN
Cuando se produce un error en el punto de conexión de red CDN de Azure por cualquier motivo, desea que la página Web toobe inteligentes suficiente tooaccess su servidor Web de origen como opción de reserva de hello para la carga de JavaScript o arranque. Es lo suficientemente grave como toolose imágenes en el sitio Web debido a falta de disponibilidad de tooCDN, pero mucho más grave funcionalidad de página fundamental de toolose proporcionada por los scripts y hojas de estilos.

Hola [agrupación](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) clase contiene una propiedad denominada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que permite el mecanismo de reserva de hello tooconfigure error de red CDN. toouse esta propiedad, siga los pasos de Hola a continuación:

1. En su proyecto de rol Web, abra *App_Start\BundleConfig.cs*, que ha agregado una dirección URL de la red CDN en cada [constructor agrupación](http://msdn.microsoft.com/library/jj646464.aspx)y realice el siguiente Hola resaltado cambia tooadd mecanismo de reserva toohello agrupaciones de forma predeterminada:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Cuando `CdnFallbackExpression` es no es null, secuencia de comandos se aplica en tootest Hola HTML si la agrupación de Hola se ha cargado correctamente y, si no es así, obtener acceso a Hola paquete directamente desde el servidor Web de origen de Hola. Esta propiedad debe toobe conjunto tooa JavaScript expresión que comprueba si el paquete de red CDN respectivo Hola está cargado correctamente. expresión de Hello necesarios tootest difiere de cada paquete de contenido de toohello correspondiente. Para paquetes de forma predeterminada Hola anteriores:
   
   * `window.jquery` se define en jquery-{version}.js
   * `$.validator` se define en jquery.validate.js
   * `window.Modernizr` se define en modernizer-{version}.js
   * `$.fn.modal` se define en bootstrap.js
     
     Puede que haya observado que no establecido CdnFallbackExpression para hello `~/Cointent/css` agrupación. Esto es porque actualmente hay un [error en System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) que inserta un `<script>` etiqueta para hello espera reserva CSS en lugar de hello `<link>` etiqueta.
     
     Sin embargo, existe una buena [solución de reserva de paquetes de estilo](https://github.com/EmberConsultingGroup/StyleBundleFallback) que ofrece [Ember Consulting Group](https://github.com/EmberConsultingGroup).
2. solución de Hola de toouse de CSS, cree un nuevo archivo .cs en su proyecto de rol Web *App_Start* carpeta denominada *StyleBundleExtensions.cs*y reemplazar su contenido con hello [código GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. En *App_Start\StyleFundleExtensions.cs*, cambiar el nombre del rol de hello espacio de nombres tooyour Web (por ejemplo, **WebRole1**).
4. Vuelva demasiado`App_Start\BundleConfig.cs` y modificar Hola última `bundles.Add` instrucción con hello después el código que aparece resaltado:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Este nuevo método de extensión usa Hola misma idea tooinject script Hola HTML toocheck Hola DOM para hello una coincidencia de nombre de clase, el nombre de la regla y el valor de regla definidos en la agrupación CSS de Hola y corresponden a las fechas toohello back-origen Web server si se produce un error de coincidencia de hello toofind.
5. Publicar servicio en la nube Hola nuevo y página principal de Hola de acceso.
6. Hola de la vista código HTML de la página de Hola. Debería encontrar scripts insertado similar toohello siguiente:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Tenga en cuenta que script insertado para agrupación CSS de hello todavía contiene restantes malicioso de Hola de hello `CdnFallbackExpression` propiedad en línea hello:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Pero, puesto que la primera parte de Hola de hello || expresión siempre devolverá true (en línea hello directamente encima), función de la sección de hello nunca se ejecutará.

## <a name="more-information"></a>Más información
* [Información general de hello red de entrega de contenido (CDN) de Azure](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Uso de CDN de Azure](cdn-create-new-endpoint.md)
* [Unión y minificación de ASP.NET](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
