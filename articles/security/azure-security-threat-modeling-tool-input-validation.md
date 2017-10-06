---
title: "aaaInput validación - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft"
description: mitigaciones en busca de amenazas que se exponen en hello herramienta de modelado de amenazas
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>Marco de seguridad: Validación de entrada | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Aplicación web** | <ul><li>[Deshabilite el scripting XSLT para todas las transformaciones mediante hojas de estilos no de confianza](#disable-xslt)</li><li>[Compruebe que cada página que pueda incluir contenido controlable por el usuario quede excluida del rastreo de MIME automático](#out-sniffing)</li><li>[Proteja o deshabilite la resolución de entidades XML](#xml-resolution)</li><li>[Las aplicaciones que usan http.sys realizan la comprobación de canonización de URL](#app-verification)</li><li>[Asegúrese de que los controles adecuados estén en vigor al aceptar archivos de usuarios](#controls-users)</li><li>[Asegúrese de que se usen parámetros con seguridad de tipos en la aplicación web para el acceso a datos](#typesafe)</li><li>[Usar las clases de enlace de modelo independiente o una vulnerabilidad de tooprevent MVC asignación masivo de listas de filtros de enlace](#binding-mvc)</li><li>[Codificar toorendering anteriores de salida de web no es de confianza](#rendering)</li><li>[Lleve a cabo la validación de entrada y el filtrado para todas las propiedades de modelo de tipo cadena](#typemodel)</li><li>[Se debería aplicar la comprobación de estado a los campos de formulario que acepten todos los caracteres, por ejemplo, editor de texto enriquecido](#richtext)</li><li>[No se asignan toosinks de elementos DOM que no tienen una codificación integradas](#inbuilt-encode)</li><li>[Todas las validar redirecciones dentro de la aplicación hello están cerradas o se realiza de forma segura](#redirect-safe)</li><li>[Implemente la validación de entrada en todos los parámetros de tipo cadena aceptados por métodos de controlador](#string-method)</li><li>[Establecer tiempo de espera de límite superior para procesar DoS tooprevent debido a las expresiones regulares toobad de expresión regular](#dos-expression)</li><li>[No use Html.Raw en las vistas Razor](#html-razor)</li></ul> | 
| **Base de datos** | <ul><li>[No use consultas dinámicas en procedimientos almacenados](#stored-proc)</li></ul> |
| **API web** | <ul><li>[Asegúrese de que se lleve a cabo la validación del modelo en métodos de API web](#validation-api)</li><li>[Implemente la validación de entrada en todos los parámetros de tipo cadena aceptados por métodos de API web](#string-api)</li><li>[Asegúrese de que se usen parámetros con seguridad de tipos en la API web para el acceso a datos](#typesafe-api)</li></ul> | 
| **Azure Document DB** | <ul><li>[Use consultas SQL parametrizadas para DocumentDB](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[Validación de entrada de WCF mediante enlaces de esquema](#schema-binding)</li><li>[Validación de entrada de WCF mediante inspectores de parámetros](#parameters)</li></ul> |

## <a id="disable-xslt"></a>Deshabilite el scripting XSLT para todas las transformaciones mediante hojas de estilos no de confianza

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Seguridad XSLT](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [Propiedad XsltSettings.EnableScript](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **Pasos** | XSLT es compatible con scripting dentro de hojas de estilos utilizando hello `<msxml:script>` elemento. Esto permite toobe de funciones personalizadas que se usa en una transformación XSLT. Hola script se ejecuta en contexto de hello del proceso de hello realizar transformación Hola. Secuencia de comandos XSLT debe deshabilitarse en una ejecución de tooprevent de entorno de confianza del código no seguro. *Si usa .NET:* el script XSLT está deshabilitado de forma predeterminada; sin embargo, debe asegurarse de que no se está explícitamente habilitada a través de hello `XsltSettings.EnableScript` propiedad.|

### <a name="example"></a>Ejemplo 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Ejemplo
Si se usa con MSXML 6.0, el script XSLT está deshabilitado de forma predeterminada; Sin embargo, debe asegurarse de que no se está explícitamente habilitada a través de la propiedad de objeto DOM XML de hello AllowXsltScript. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Ejemplo
Si usa MSXML 5 o una versión anterior, el scripting XSLT está habilitado de forma predeterminada y debe deshabilitarlo explícitamente. Establecer Hola DOM XML objeto propiedad AllowXsltScript toofalse. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>Compruebe que cada página que pueda incluir contenido controlable por el usuario quede excluida del rastreo de MIME automático

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [IE8 Security Part V - Comprehensive Protection](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx) (Seguridad de IE8 (parte V): Protección completa)  |
| **Pasos** | <p>Para cada página que podría incluir contenido controlable de usuario, debe usar hello encabezado HTTP `X-Content-Type-Options:nosniff`. toocomply con este requisito, puede cualquier encabezado necesaria del conjunto Hola de página por página para únicamente aquellas páginas que podrían incluir contenido controlable por el usuario, o puede establecer globalmente para todas las páginas de aplicación hello.</p><p>Cada tipo de archivo que se vaya a entregar desde un servidor web tiene asociado un [tipo MIME](http://en.wikipedia.org/wiki/Mime_type) (también denominado una *tipo de contenido*) que describe la naturaleza de Hola de contenido de hello (es decir, imagen, texto, aplicación, etcetera.)</p><p>encabezado de Hello X-contenido-opciones de tipo es un encabezado HTTP que permite a los desarrolladores toospecify que su contenido no debería estar examinan MIME. Este encabezado es toomitigate diseñada ataques de examen de MIME. Se agregó compatibilidad con este encabezado en Internet Explorer 8 (IE8).</p><p>Los únicos que se beneficiarán de X-Content-Type-Options son los usuarios de Internet Explorer 8 (IE8). Las versiones anteriores de Internet Explorer no respetan actualmente el encabezado X-contenido-opciones de tipo de Hola</p><p>Internet Explorer 8 (y versiones posterior) son Hola principales exploradores tooimplement un examen de MIME Cancelar voluntariamente la característica. Cuando otros exploradores principales (Firefox, Safari, Chrome) implementan características similares, esta recomendación será sintaxis tooinclude actualizada para dichos exploradores también</p>|

### <a name="example"></a>Ejemplo
encabezado necesario de Hola de tooenable globalmente para todas las páginas de aplicación hello, siga uno de los siguientes hello: 

* Agregar encabezado de hello en el archivo web.config de hello si aplicación hello está hospedado por Internet Information Services (IIS) 7 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Agregar encabezado de Hola a través de hello global de la aplicación\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* Implemente un módulo HTTP personalizado 

``` 
public class XContentTypeOptionsModule : IHttpModule 
  {
    #region IHttpModule Members 
    public void Dispose() 
    { 

    } 
    public void Init(HttpApplication context)
    { 
      context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders); 
    } 
    #endregion 
    void context_PreSendRequestHeaders(object sender, EventArgs e) 
      { 
        HttpApplication application = sender as HttpApplication; 
        if (application == null) 
          return; 
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* Puede habilitar el encabezado necesario de hello solo para páginas específicas mediante la adición de las respuestas de tooindividual: 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>Proteja o deshabilite la resolución de entidades XML

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [XML Entity Expansion](http://capec.mitre.org/data/definitions/197.html) (Expansión de entidad XML), [Ataques por denegación de servicio y defensas XML](http://msdn.microsoft.com/magazine/ee335713.aspx), [Información general de seguridad MSXML](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [Prácticas recomendadas para proteger el código MSXML](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [NSXMLParserDelegate Protocol Reference](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html) (Referencia del protocolo NSXMLParserDelegate), [Resolver recursos externos](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **Pasos**| <p>Aunque no se usa ampliamente, hay una característica de XML que permite tooexpand de analizador XML de hello entidades de macro con valores definidos en el propio documento Hola o de orígenes externos. Por ejemplo, documento Hola podría definir una entidad "companyname" con el valor de Hola "Microsoft", para que cada vez Hola texto "&companyname;" aparece en el documento de hello, será sustituido automáticamente con el texto hello Microsoft. O bien, documento Hola podría definir una entidad "MSFTStock", lo que hace referencia a un web externo servicio toofetch Hola valor actual de acciones de Microsoft.</p><p>A continuación, en cualquier momento "&MSFTStock;" aparece en el documento hello, será sustituido automáticamente con el precio de las acciones por hello actual. Sin embargo, esta funcionalidad puede ser toocreate abusa condiciones de denegación de servicio (DoS). Un atacante puede anidar varias entidades toocreate una bomba XML de expansión exponencial que consuma toda la memoria disponible en el sistema de Hola. </p><p>Como alternativa, puede crear una referencia externa que transmita por secuencias back una cantidad infinita de datos o simplemente bloquea el subproceso de Hola. Como resultado, deben deshabilitar todos los equipos interna o externa resolución de entidad XML completamente si su aplicación no usar, o manualmente limitar la cantidad de Hola de memoria y tiempo de aplicación hello puede consumir para la resolución de entidad si esta funcionalidad es sea absolutamente necesario. Si la aplicación no necesita la resolución de entidades, deshabilítela. </p>|

### <a name="example"></a>Ejemplo
Para el código de .NET Framework, puede usar Hola siguientes enfoques:

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
Tenga en cuenta que este valor predeterminado Hola de `ProhibitDtd` en `XmlReaderSettings` es true, pero en `XmlTextReader` es false. Si usas XmlReaderSettings, no es necesario tooset ProhibitDtd tootrue explícitamente, pero se recomienda que realice para simplificar de seguridad. También tenga en cuenta que Hola clase XmlDocument permite que la resolución de entidad de forma predeterminada. 

### <a name="example"></a>Ejemplo
resolución de entidades de toodisable para XmlDocuments, use hello `XmlDocument.Load(XmlReader)` sobrecarga de hello Load (método) y establecer Hola propiedades correspondientes en la resolución de toodisable de argumento de XmlReader hello, como se muestra en el siguiente código de hello: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>Ejemplo
Si no es posible que la aplicación deshabilitar resolución de entidades, establezca hello XmlReaderSettings.MaxCharactersFromEntities propiedad tooa valor razonable según las necesidades de la aplicación tooyour. Esto limitará el impacto de Hola de posibles ataques de denegación de expansión exponencial. Hola siguiente código proporciona un ejemplo de este enfoque: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>Ejemplo
Si necesita tooresolve alineado entidades, pero no es necesario tooresolve las entidades externas, establezca hello XmlReaderSettings.XmlResolver propiedad toonull. Por ejemplo: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Tenga en cuenta que en MSXML6, ProhibitDTD se establece tootrue (deshabilitar el procesamiento de DTD) de forma predeterminada. Para el código de Apple OSX e iOS, puede usar uno de estos dos analizadores XML: NSXMLParser y libXML2. 

## <a id="app-verification"></a>Las aplicaciones que usan http.sys realizan la comprobación de canonización de URL

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Cualquier aplicación que use http.sys debe seguir estas instrucciones:</p><ul><li>Limitar toono de longitud de dirección URL de hello más de 16.384 caracteres (ASCII o Unicode). Se trata de hello absoluta URL longitud máxima en función de configuración de Internet Information Services (IIS) 6 de hello predeterminada. Se debe procurar que los sitios web usen direcciones URL más cortas, de ser posible.</li><li>Utilizar clases de E/S de archivos de .NET Framework estándares de hello (por ejemplo, FileStream) como estos aprovechará hello las reglas de canonización en hello .NET FX</li><li>Cree explícitamente una lista de nombres de archivo conocidos permitidos.</li><li>Rechace de forma explícita los tipos de archivo conocidos a los que no servirá rechazos de UrlScan: archivos exe, bat, cmd, com, htw, ida, idq, htr, idc, shtm[l], stm, ini, pol, dat y de impresora.</li><li>Detectar Hola siguientes excepciones:<ul><li>System.ArgumentException (para nombres de dispositivo)</li><li>System.NotSupportedException (para flujos de datos)</li><li>System.IO.FileNotFoundException (para nombres de archivo con escape no válidos)</li><li>System.IO.DirectoryNotFoundException (para directorios con escape no válidos)</li></ul></li><li>*No* destacar tooWin32 archivo I/O APIs. En una dirección URL no válida devolver correctamente un usuario de 400 error toohello y registrar error real Hola.</li></ul>|

## <a id="controls-users"></a>Asegúrese de que los controles adecuados estén en vigor al aceptar archivos de usuarios

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Unrestricted File Upload](https://www.owasp.org/index.php/Unrestricted_File_Upload) (Carga de archivos sin restricciones), [File Signature Table](http://www.garykessler.net/library/file_sigs.html) (Tabla de firmas de archivo) |
| **Pasos** | <p>Los archivos cargados representan un riesgo significativo tooapplications.</p><p>primer paso de Hello en muchos ataques es tooget atacada algunos toobe de sistema de toohello de código. A continuación, ataque Hola solo necesita toofind ejecuta un código de hello tooget de manera. El uso de una carga de archivos ayuda a atacante Hola realizar el primer paso de Hola. pueden variar consecuencias Hola de carga de archivos sin restricciones, incluyendo adquisición de sistema completo, un sistema de archivos sobrecargado o la base de datos, tooback los sistemas de ataques y simple asalto de reenvío.</p><p>Depende de la aplicación hello no con el archivo hello cargado y especialmente donde se almacena. Falta la validación del lado servidor para las cargas de archivos. Se deberían implementar los siguientes controles de seguridad para la funcionalidad de carga de archivos:</p><ul><li>Comprobación de la extensión del archivo (solo se debe aceptar un conjunto válido de tipos de archivo permitidos)</li><li>Límite máximo de tamaño de archivo</li><li>Archivo no debe estar cargado toowebroot; ubicación de Hello debe ser un directorio en la unidad del sistema no</li><li>Convención de nomenclatura debe seguir esa hello nombre del archivo cargado tienen algunas aleatoriedad, por lo que como tooprevent sobrescribe el archivo</li><li>Se deben analizar archivos de programa antivirus antes de escribir en disco toohello</li><li>Asegúrese de que el nombre de archivo de Hola y cualquier otro metadato (p. ej., ruta de acceso de archivo) se validan para caracteres malintencionados</li><li>Debe comprobarse la firma del archivo de formato, un usuario de cargar un archivo enmascarado tooprevent (p. ej., cargando un archivo exe cambiando tootxt de extensión)</li></ul>| 

### <a name="example"></a>Ejemplo
Para el último punto de hello relacionado con la validación de firma de formato de archivo, consulte la clase toohello a continuación para obtener más información: 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>Asegúrese de que se usen parámetros con seguridad de tipos en la aplicación web para el acceso a datos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Si utiliza la colección de parámetros de hello, SQL trata Hola entrada es como un valor literal en lugar de en código ejecutable. Hola colección de parámetros puede ser tooenforce usado las restricciones de tipo y longitud de los datos de entrada. Valores fuera de intervalo de hello desencadenan una excepción. Si no se utilizan parámetros SQL de seguridad de tipos, los atacantes podrían tooexecute capaz de ataques de inyección que se incrustan en la entrada de hello sin filtrar.</p><p>Usar parámetros de tipo seguro cuando construir SQL las consultas tooavoid posibles ataques de inyección SQL que pueden producirse con una entrada sin filtrar. Puede usar parámetros con seguridad de tipos con procedimientos almacenados e instrucciones SQL dinámicas. Los parámetros se tratan como valores literales por base de datos de hello y no como código ejecutable. También se comprueban el tipo y la longitud de los parámetros.</p>|

### <a name="example"></a>Ejemplo 
Hello código siguiente muestra cómo toouse parámetros de tipo seguros con hello SqlParameterCollection al llamar a un procedimiento almacenado. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Hola anterior ejemplo de código, el valor de entrada de hello no puede ser más de 11 caracteres. Si no ajustan datos hello toohello tipo o la longitud definida por el parámetro hello, Hola SqlParameter (clase) inicia una excepción. 

## <a id="binding-mvc"></a>Usar las clases de enlace de modelo independiente o una vulnerabilidad de tooprevent MVC asignación masivo de listas de filtros de enlace

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Atributos de metadatos](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [pública clave de seguridad y mitigación de vulnerabilidades](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [tooMass guía completa la asignación en ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [Introducción a EF mediante MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **Pasos** | <ul><li>**¿Cuándo debería buscar vulnerabilidades por publicación excesiva?** Las vulnerabilidades por publicación excesiva se pueden producir en cualquier lugar donde se enlacen clases de modelo desde la entrada del usuario. Los marcos de trabajo como MVC pueden representar datos de usuario en clases .NET personalizadas, incluidos los objetos CLR estándar (POCO). MVC rellena automáticamente estas clases de modelo con datos de solicitud de hello, que proporciona una representación adecuada para tratar los proporcionados por el usuario. Cuando estas clases incluyen propiedades que no se deben establecer usuario hello, aplicación hello puede ser vulnerables ataques tooover registro, que permiten el control de usuario de datos que nunca la aplicación hello diseñada. Como el enlace de modelo MVC, tecnologías de acceso de la base de datos como objeto/relacional asignadores como Entity Framework a menudo también admiten el uso POCO objetos toorepresent bases de datos. Estas clases de modelo de datos proporcionan Hola mismo comodidad en tratar con datos de la base de datos como MVC hace para manejar de proporcionados por el usuario. Porque la base de datos de hello y MVC admite modelos similares, como los objetos POCO, parece hello tooreuse fácil mismo clases ambos fines. Se produce un error en esta práctica toopreserve separación de aspectos y es un área común donde imprevistos propiedades son expuestas toomodel enlace, habilitar el registro excesivo ataques.</li><li>**¿¿Por qué no usar mis clases de modelo de base de datos sin filtrar como acciones de MVC toomy parámetros? -** Enlace del modelo MVC porque se enlazará nada en esa clase. Incluso si los datos no aparecen en la vista, que un usuario malintencionado puede enviar una solicitud HTTP con estos datos incluidos de Hola y MVC con gusto enlazará, porque la acción indica que la clase de base de datos es forma Hola de los datos debe aceptar proporcionados por el usuario.</li><li>**¿Por qué debo preocuparme forma Hola usada para el enlace del modelo? -** Enlace de modelos de uso de ASP.NET MVC con modelos demasiado amplios expone un ataques de tooover-registro de aplicación. Registro excesivo podría permitir a datos de la aplicación de los atacantes toochange más allá de qué developer Hola prevista, como reemplazar precio Hola un elemento o hello privilegios de seguridad de una cuenta. Las aplicaciones deben utilizar tooprovide de enlace de modelos (o listas de filtros de propiedad admitidos específico) específicos para la acción un contrato explícito para qué tooallow de entrada no es de confianza a través del enlace del modelo.</li><li>**¿Tener modelos de enlace independientes sirve solo para duplicar el código?** No, es cuestión de separar los aspectos. Si vuelve a usar modelos de base de datos en los métodos de acción, se que indica que cualquier propiedad (o secundario) en que la clase se puede establecer por usuario de hello en una solicitud HTTP. Si no lo que desea es toodo MVC, se necesita una lista de filtros o un tooshow de forma independiente de clase MVC qué datos pueden proceder de entrada en su lugar del usuario.</li><li>**Si dispongo de modelos de enlace independiente proporcionados por el usuario, ¿tengo tooduplicate mi atributos de anotación de datos? -** No necesariamente. Puede usar MetadataTypeAttribute en hello base de datos modelo clase toolink toohello metadatos en una clase de enlace del modelo. Solo tenga en cuenta que Hola Hola MetadataTypeAttribute al que hace referencia el tipo debe ser un subconjunto de Hola que hacen referencia a tipo (puede tener menos propiedades, pero no más).</li><li>**Mover los datos entre los modelos de entrada de usuario y los modelos de base de datos es una tarea tediosa. ¿Puedo simplemente copiar todas las propiedades mediante reflexión?** Sí. Hello solo las propiedades que aparecen en los modelos de enlace de hello son hello las que consideras toobe seguro para la entrada del usuario. No hay ninguna razón de seguridad que impide el uso de reflexión toocopy sobre todas las propiedades que existen en común entre estos dos modelos.</li><li>**¿Y [Bind(Exclude ="â€¦")]? ¿Lo puedo usar en lugar de tener modelos de enlace independientes?** No se recomienda este enfoque. Si se usa [Bind(Exclude ="â€¦")], quiere decir que cualquier propiedad nueva se puede enlazar de forma predeterminada. Cuando se agrega una nueva propiedad, hay un cosas de paso adicional tooremember tookeep seguro, en lugar de tener diseño Hola ser seguro de forma predeterminada. Función de desarrollador de Hola comprobación cada vez que se agrega una propiedad de esta lista es arriesgada.</li><li>**¿Es [Bind(Include ="â€¦")] útil para las operaciones de edición?** No. [Bind(Include ="â€¦")] solo vale para las operaciones de estilo INSERT (agregar datos nuevos). Para las operaciones de actualización estilo (revisión de los datos existentes), utilice otra aproximación posible, al igual que con modelos de enlace independientes o pasar una lista de propiedades permitidas tooUpdateModel o TryUpdateModel explícita. Agregar un [enlazar (Include = "â...")] significa que el atributo en una operación de edición que MVC creará una instancia de objeto y establecerá solo Hola enumera las propiedades, dejando el resto en sus valores predeterminados. Cuando se mantienen los datos de hello, reemplazará completamente entidad existente hello, restablecer los valores de hello para cualquier parámetro predeterminado tootheir de propiedades se omite. Por ejemplo, si se omite IsAdmin desde un [enlazar (Include = "â...")] atributo en una operación de edición, cualquier usuario cuyo nombre se ha editado a través de esta acción sería restablecimiento tooIsAdmin = false (cualquier usuario editado perdería estado de administrador). Si desea tooprevent actualiza las propiedades de toocertain, utilice uno de hello otros enfoques anteriormente. Tenga en cuenta que algunas versiones de las herramientas de MVC generan clases de controlador con [Bind(Include ="â€¦")] en acciones de edición e indican que la eliminación de una propiedad de esa lista impedirá los ataques por publicación excesiva. Sin embargo, como se describió anteriormente, este enfoque no funciona según lo previsto y en su lugar, se restablecerán los datos en los valores predeterminados de hello omitida propiedades tootheir.</li><li>**Para las operaciones Create, ¿hay alguna advertencia sobre el uso de [Bind(Include ="â€¦")] en lugar de modelos de enlace independientes? -** Sí. En primer lugar, este enfoque no funciona para los escenarios de edición, por lo que es necesario mantener dos enfoques independientes para mitigar todas las vulnerabilidades por publicación excesiva. Modelos de enlace en segundo lugar, independiente imponga la separación de intereses entre la forma de hello utilizada para la forma de hello y entrada de usuario utilizada para la persistencia, algo [enlazar (Include = "â...")] no lleva a cabo. En tercer lugar, tenga en cuenta que [enlazar (Include = "â...")] solo puede controlar propiedades de nivel superior; no se permiten solo algunas partes de subpropiedades (por ejemplo, "Details.Name") en el atributo de Hola. Por último y quizás lo más importante, usar [enlazar (Include = "â...")] agrega un paso adicional que se debe recordar cualquier clase de Hola de tiempo se utiliza para el enlace de modelos. Si un nuevo método de acción enlaza la clase de datos de toohello directamente y olvida tooinclude un [enlazar (Include = "â...")] atributo, puede ser vulnerable tooover contabilización ataques, por lo que Hola [enlazar (Include = "â...")] enfoque es algo menos seguro de forma predeterminada. Si usas [enlazar (Include = "â...")], tenga siempre cuidado tooremember toospecify, cada vez que las clases de datos aparecen como parámetros de método de acción.</li><li>**¿Para operaciones de creación, lo que acerca de cómo colocar Hola [enlazar (Include = "â...")] atributo en la propia clase de modelo Hola? ¿Puede evitar Hola necesidad tooremember poner Hola atributo en cada método de acción no este enfoque? -** Este enfoque funciona en algunos casos. Usar [enlazar (Include = "â...")] en el propio tipo de modelo hello (en lugar de en parámetros de acción mediante esta clase), evitar la necesidad de Hola tooremember tooinclude Hola [enlazar (Include = "â...")] atributo en cada método de acción. El uso de atributo de hello directamente en la clase hello eficazmente, crea un área expuesta independiente de esta clase para fines de enlace de modelo. Sin embargo, este enfoque solo permite una forma de enlace de modelos por cada clase de modelo. Si un método de acción debe tooallow enlace del modelo de un campo (por ejemplo, un solo administrador acción que actualiza los roles de usuario) y otras acciones deben tooprevent enlace del modelo de este campo, este enfoque no funcionará. Cada clase puede tener solamente una forma de enlace de modelo; Si las diferentes acciones necesitan formas de enlace de modelo diferente, deberá toorepresent estos separan formas mediante cualquier clases de enlace de modelo independiente o separan [enlazar (Include = "â...")] atributos en los métodos de acción de Hola.</li><li>**¿Qué son los modelos de enlace? ¿Son que Hola lo mismo que ver modelos? -** Se trata de dos conceptos relacionados. modelo de enlace hace referencia la clase de modelo de tooa usada en una acción de término de Hello es la lista de parámetros (forma de hello pasado desde el método de acción de MVC modelo enlace toohello). modelo de vista de Hello término hace referencia a clase del modelo tooa pasado de una vista de tooa de método de acción. Con un modelo específico de la vista es un enfoque común para pasar datos de una vista de tooa de método de acción. A menudo, esta forma también es adecuada para el enlace de modelos y modelo de vista de hello término puede ser hello toorefer usado mismo modelo se utiliza en ambos lugares. toobe precisa, este procedimiento se comunica específicamente sobre el enlace de modelos, centrándose en forma de hello pasado toohello acción, que es lo que realmente importa para fines de asignación masivo.</li></ul>| 

## <a id="rendering"></a>Codificar toorendering anteriores de salida de web no es de confianza

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, formularios Web Forms, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [¿Cómo tooprevent Cross-site scripting en ASP.NET](http://msdn.microsoft.com/library/ms998274.aspx), [el Scripting entre sitios](http://cwe.mitre.org/data/definitions/79.html), [hoja de referencia rápida de prevención de XSS (Cross Site Scripting)](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **Pasos** | Scripting entre sitios (normalmente abreviado como XSS) es un vector de ataque de servicios en línea o cualquier aplicación o el componente que procesa entradas desde web Hola. Vulnerabilidades XSS pueden permitir que un atacante tooexecute script en el equipo del otro usuario a través de una aplicación web sea vulnerable. Scripts malintencionados pueden toosteal usa cookies y alterar en caso contrario, un equipo infectado a través de JavaScript. Se impide el XSS mediante la validación de la entrada del usuario para asegurarse de que esté bien formada y codificada antes de representarla en una página web. La validación de la entrada y la codificación de la salida se pueden realizar con Web Protection Library. Para código administrado (C\#, VB.net, etc.), utilice uno o más adecuados los métodos de codificación de hello biblioteca Web protección (Anti-XSS), según el contexto de Hola donde obtiene manifiesta Hola proporcionados por el usuario:| 

### <a name="example"></a>Ejemplo

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>Lleve a cabo la validación de entrada y el filtrado para todas las propiedades de modelo de tipo cadena

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Adding Validation](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation) (Incorporación de validación), [Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx) (Validación de datos de modelo en una aplicación de MVC), [Principios orientativos para las aplicaciones de ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Pasos** | <p>Todos los parámetros de entrada de hello deben validarse antes de que se utilizan en tooensure de aplicación Hola que aplicación hello protegida frente a las entradas de usuario malintencionado. Validar valores de entrada de hello mediante validaciones de expresión regular en el lado del servidor con una estrategia de validación de la lista blanca. Unsanitized entradas de usuario / parámetros pasados a métodos de toohello pueden originar código vulnerabilidades por inyección de código.</p><p>Para las aplicaciones web, los puntos de entrada también pueden ser campos de formulario, QueryStrings, cookies, encabezados HTTP y parámetros de servicio web.</p><p>Hello siguientes comprobaciones de validación de entrada se deben realizar en el enlace de modelos:</p><ul><li>propiedades del modelo Hola deben anotarse con la anotación de expresión regular, para aceptar caracteres permitidos y la longitud máxima permitida</li><li>los métodos de controlador de Hello deben realizar ModelState validez</li></ul>|

## <a id="richtext"></a>Se debería aplicar la comprobación de estado a los campos de formulario que acepten todos los caracteres, por ejemplo, editor de texto enriquecido

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Codificación de la entrada no segura](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3), [HTMLSanitizer](https://github.com/mganss/HtmlSanitizer) |
| **Pasos** | <p>Identifique todas las etiquetas de marcado estático que desea toouse. Una práctica común es toorestrict elementos de formato toosafe HTML, como `<b>` (negrita) y `<i>` (cursiva).</p><p>Antes de escribir datos de hello, codificar en HTML. Esto hace que cualquier script malintencionado seguro haciendo toobe trata como texto, no como código ejecutable.</p><ol><li>Deshabilitar la solicitud ASP.NET validación agregando Hola Hola ValidateRequest = "false" atributo toohello directiva @ Page</li><li>Codificar la entrada de cadena de hello con método hello</li><li>Utilizar un StringBuilder y una llamada a su tooselectively de método de reemplazo quitar Hola codificación en elementos de hello HTML que desea toopermit</li></ol><p>Hola Hola en página referencias deshabilita la validación de solicitudes ASP.NET estableciendo `ValidateRequest="false"`. Se codifica en HTML Hola de entrada y permite de forma selectiva hello `<b>` y `<i>` o bien, una biblioteca de .NET para la comprobación de estado HTML también puede utilizarse.</p><p>HtmlSanitizer es una biblioteca de .NET para la limpieza de documentos de construcciones que pueden dar lugar a ataques de tooXSS y fragmentos HTML. Usa AngleSharp tooparse, manipular y presentar HTML y CSS. HtmlSanitizer puede instalarse como un paquete de NuGet, y se pueden pasar Hola proporcionados por el usuario a través de HTML o CSS inmunización métodos pertinentes, según corresponda, en el lado del servidor de Hola. Tenga en cuenta que la comprobación de estado como control de seguridad se debe considerar la última opción.</p><p>La validación de entrada y la codificación de salida son los controles de seguridad que se consideran mejores.</p> |

## <a id="inbuilt-encode"></a>No se asignan toosinks de elementos DOM que no tienen una codificación integradas

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Muchas funciones JavaScript no codifican de forma predeterminada. Al asignar elementos de tooDOM de entrada no es de confianza a través de estas funciones, puede producir entre ejecuciones de secuencias de comandos (XSS) de sitio.| 

### <a name="example"></a>Ejemplo
Los siguientes son ejemplos inseguros: 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
No utilice `innerHtml`; en su lugar, use `innerText`. Igualmente, en lugar de `$("#elm").html()`, use `$("#elm").text()`. 

## <a id="redirect-safe"></a>Todas las validar redirecciones dentro de la aplicación hello están cerradas o se realiza de forma segura

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Hola marco de autorización de OAuth 2.0 - redirectores abierto](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **Pasos** | <p>Diseño de aplicaciones que requieren la ubicación de redirección tooa proporcionado por el usuario debe restringir Hola redirección posibles destinos tooa "seguro" lista predefinida de sitios o dominios. Todas las redirecciones de la aplicación hello deben ser cerrado o seguridad.</p><p>toodo esto:</p><ul><li>Identifique todos los redireccionamientos.</li><li>Implemente una mitigación adecuada para cada tipo de redireccionamiento. Entre las mitigaciones adecuadas, se incluye la lista de redireccionamientos permitidos o la confirmación del usuario. Si un sitio web o servicio con una vulnerabilidad de redireccionamiento abierto usa proveedores de identidades de Facebook, OAuth u OpenID, un atacante puede robar el token de inicio de sesión de un usuario y suplantarle. Esto es un riesgo inherente al utilizar OAuth, que se describe en RFC 6749 "hello marco de autorización OAuth 2.0", sección 10.15 "abrir redirige" de forma similar, las credenciales de los usuarios pueden estar en peligro por ataques de suplantación de identidad de ataques mediante redirecciones abiertas</li></ul>|

## <a id="string-method"></a>Implemente la validación de entrada en todos los parámetros de tipo cadena aceptados por métodos de controlador

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx) (Validación de datos de modelo en una aplicación de MVC), [Principios orientativos para las aplicaciones de ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Pasos** | Para los métodos que solo acepten el tipo primitivo de datos como argumento, pero no modelos, se debe realizar la validación de entrada mediante expresiones regulares. Aquí se debería usar Regex.IsMatch con un patrón de regex válido. Si no coincide con la entrada de Hola Hola expresión Regular especificada, control no debe continuar y se debe mostrar una advertencia adecuada con respecto a los errores de validación.| 

## <a id="dos-expression"></a>Establecer tiempo de espera de límite superior para procesar DoS tooprevent debido a las expresiones regulares toobad de expresión regular

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, formularios Web Forms, MVC5, MVC6  |
| **Atributos**              | N/D  |
| **Referencias**              | [Propiedad DefaultRegexMatchTimeout](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **Pasos** | tooensure ataques por denegación de servicio contra mal crear expresiones regulares, que provocan grandes tiempos de retroceso, establecer el tiempo de espera de hello predeterminado global. Si el tiempo de procesamiento de hello tarda más tiempo de hello define el límite superior, produciría una excepción de tiempo de espera. Si se configura nada, tiempo de espera de hello sería infinito.| 

### <a name="example"></a>Ejemplo
Por ejemplo, hello configuración siguiente producirá un RegexMatchTimeoutException, si el procesamiento de hello tarda más de 5 segundos: 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>No use Html.Raw en las vistas Razor

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| Paso | Las páginas Web ASP.Net (Razor) realizan la codificación de HTML automáticamente. Todas las cadenas impresas por fragmentos de código insertados (bloques @) se codifican en HTML de forma automática. Sin embargo, cuando se invoca el método `HtmlHelper.Raw`, devuelve marcado que no está codificado en HTML. Si `Html.Raw()` se utiliza el método auxiliar, omite Hola codificación la protección automática que proporciona Razor.|

### <a name="example"></a>Ejemplo
El siguiente ejemplo es inseguro: 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
No utilice `Html.Raw()` a menos que necesite toodisplay marcado. Este método no realiza la codificación de salida implícitamente. Use otros métodos auxiliares de ASP.NET, como `@Html.DisplayFor()`. 

## <a id="stored-proc"></a>No use consultas dinámicas en procedimientos almacenados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Un ataque de inyección de SQL aprovecha las vulnerabilidades en comandos arbitrarios de validación de entrada toorun en base de datos de Hola. Puede producirse cuando la aplicación utiliza la entrada tooconstruct dinámica tooaccess de instrucciones SQL Hola base de datos. También puede producirse si el código usa procedimientos almacenados a los que se pasan cadenas que contienen entrada de usuario sin procesar. Mediante Hola ataque de inyección de SQL, atacante Hola puede ejecutar comandos arbitrarios en la base de datos de Hola. Todas las instrucciones de SQL (incluidas las instrucciones de SQL de hello en los procedimientos almacenados) deben tener parámetros. Instrucciones SQL parametrizadas aceptará caracteres que tienen un significado especial tooSQL (por ejemplo, las comillas simples) sin problemas porque están fuertemente tipados. |

### <a name="example"></a>Ejemplo
El ejemplo siguiente es de un procedimiento almacenado dinámico inseguro: 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>Ejemplo
Aquí te mostramos Hola mismo procedimiento almacenado se implementa de forma segura: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>Asegúrese de que se lleve a cabo la validación del modelo en métodos de API web

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) (Validación de modelo en ASP.NET Web API) |
| **Pasos** | Cuando un cliente envía API web de tooa de datos, son obligatorios toovalidate Hola datos antes de realizar cualquier procesamiento. Para ASP.NET Web API que aceptan modelos como entrada, utilice las anotaciones de datos en las reglas de validación de modelos tooset en Propiedades de Hola de modelo de Hola.|

### <a name="example"></a>Ejemplo
Hola siguiente código de muestra de Hola mismo: 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>Ejemplo
En el método de acción de Hola de controladores de API de Hola, validez del modelo de hello tiene toobe comprueban explícitamente como se muestra a continuación: 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Implemente la validación de entrada en todos los parámetros de tipo cadena aceptados por métodos de API web

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, MVC 5, MVC 6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Validating Model Data in an MVC Application](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx) (Validación de datos de modelo en una aplicación de MVC), [Principios orientativos para las aplicaciones de ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Pasos** | Para los métodos que solo acepten el tipo primitivo de datos como argumento, pero no modelos, se debe realizar la validación de entrada mediante expresiones regulares. Aquí se debería usar Regex.IsMatch con un patrón de regex válido. Si no coincide con la entrada de Hola Hola expresión Regular especificada, control no debe continuar y se debe mostrar una advertencia adecuada con respecto a los errores de validación.|

## <a id="typesafe-api"></a>Asegúrese de que se usen parámetros con seguridad de tipos en la API web para el acceso a datos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Si utiliza la colección de parámetros de hello, SQL trata Hola entrada es como un valor literal en lugar de en código ejecutable. Hola colección de parámetros puede ser tooenforce usado las restricciones de tipo y longitud de los datos de entrada. Valores fuera de intervalo de hello desencadenan una excepción. Si no se utilizan parámetros SQL de seguridad de tipos, los atacantes podrían tooexecute capaz de ataques de inyección que se incrustan en la entrada de hello sin filtrar.</p><p>Usar parámetros de tipo seguro cuando construir SQL las consultas tooavoid posibles ataques de inyección SQL que pueden producirse con una entrada sin filtrar. Puede usar parámetros con seguridad de tipos con procedimientos almacenados e instrucciones SQL dinámicas. Los parámetros se tratan como valores literales por base de datos de hello y no como código ejecutable. También se comprueban el tipo y la longitud de los parámetros.</p>|

### <a name="example"></a>Ejemplo
Hello código siguiente muestra cómo toouse parámetros de tipo seguros con hello SqlParameterCollection al llamar a un procedimiento almacenado. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Hola anterior ejemplo de código, el valor de entrada de hello no puede ser más de 11 caracteres. Si no ajustan datos hello toohello tipo o la longitud definida por el parámetro hello, Hola SqlParameter (clase) inicia una excepción. 

## <a id="sql-docdb"></a>Uso de consultas SQL parametrizadas con Cosmos DB

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Announcing SQL Parameterization in DocumentDB](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) (Anuncio de la parametrización de SQL en DocumentDB) |
| **Pasos** | Aunque DocumentDB solo admite consultas de solo lectura, todavía es posible inyectar código SQL si las consultas se crean mediante la concatenación con la entrada del usuario. Es posible que un toodata de acceso de usuario toogain que no deberían tener acceso a dentro de Hola misma colección diseñando consultas SQL malintencionadas. Use consultas SQL parametrizadas si las consultas se construyen tomando como base la entrada del usuario. |

## <a id="schema-binding"></a>Validación de entrada de WCF mediante enlaces de esquema

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **Pasos** | <p>Falta de validación da lugar a ataques de inyección de código de tipo toodifferent.</p><p>Validación del mensaje representa una línea de defensa para la protección de saludo de la aplicación de WCF. Con este enfoque, validar mensajes mediante operaciones de servicio WCF de esquemas tooprotect contra los ataques de un cliente malintencionado. Validar todos los mensajes recibidos por hello tooprotect Hola cliente contra los ataques por un servicio malintencionado. Validación del mensaje hace posible toovalidate mensajes cuando las operaciones de consumir contratos de mensajes o contratos de datos, lo que no se puede realizar mediante la validación de parámetros. Validación de mensajes le permite toocreate lógica de validación en esquemas, con lo que se proporciona más flexibilidad y reducir el tiempo de desarrollo. Los esquemas se pueden reutilizar en las distintas aplicaciones dentro de la organización de hello, creación de estándares para la representación de datos. Además, validación de mensajes le permite operaciones de tooprotect cuando usan tipos de datos más complejos que implican contratos que representa la lógica de negocios.</p><p>validación del mensaje tooperform, primero cree un esquema que representa las operaciones de Hola de los tipos de datos de hello y servicio utilizados por esas operaciones. A continuación, cree una clase de .NET que implementa un inspector de mensajes de cliente personalizada y distribuidor personalizado de mensajes inspector toovalidate Hola de mensajes enviados o recibidos desde el servicio de Hola. A continuación, implemente una validación de mensajes de tooenable de comportamiento de extremo personalizado en el cliente de Hola y el servicio de Hola. Por último, implementar un elemento de configuración personalizada en una clase hello que permite tooexpose hello extendido comportamiento de extremo personalizado en archivo de configuración de hello del servicio de Hola o cliente de hello"</p>|

## <a id="parameters"></a>Validación de entrada de WCF mediante inspectores de parámetros

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **Pasos** | <p>Entrada y validación de datos representa una línea de defensa en protección de saludo de la aplicación WCF importante. Debe validar todos los parámetros que se exponen en el servicio WCF servicio operations tooprotect Hola contra los ataques mediante un cliente malintencionado. A la inversa, también debe validar todos los valores devueltos recibidos por hello tooprotect Hola cliente contra los ataques por un servicio malintencionado</p><p>WCF ofrece puntos de extensibilidad diferentes que permiten el comportamiento de tiempo de ejecución WCF de hello toocustomize mediante la creación de extensiones personalizadas. Los inspectores y los inspectores de parámetros son dos mecanismos de extensibilidad de mensaje utiliza toogain mayor control sobre los datos de hello pasar entre un cliente y un servicio. Debe usar los inspectores de parámetros para la validación de entrada y usar los inspectores de mensaje sólo cuando sea necesario que fluyen dentro y fuera de un servicio de todo mensaje tooinspect Hola.</p><p>tooperform la validación de entrada, generará una clase .NET e implementar un inspector de parámetros personalizado en los parámetros de toovalidate de orden de las operaciones en el servicio. A continuación, implementará una validación de tooenable del comportamiento de extremo personalizado en el cliente de Hola y el servicio de Hola. Por último, implementará un elemento de configuración personalizado en una clase hello que permite tooexpose hello extendido comportamiento de extremo personalizado en archivo de configuración de hello del servicio de Hola o cliente de Hola</p>|
