---
title: "Guía de programación de aaaU-SQL de Azure Data Lake | Documentos de Microsoft"
description: "Obtenga información sobre el conjunto de hello de servicios de Azure Data Lake que le permiten toocreate una plataforma de grandes cantidades de datos en la nube."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a>Guía de programación de U-SQL

U-SQL es un lenguaje de consulta diseñado para tipo de macrodatos de cargas de trabajo. Una de las características únicas de Hola de U-SQL es la combinación de Hola de lenguaje declarativo de hello similar a SQL con la extensibilidad de Hola y capacidad de programación que se proporciona en C#. En esta guía, se concentrarse en la extensibilidad de Hola y capacidad de programación del lenguaje de U-SQL de Hola que está habilitada en C#.

## <a name="requirements"></a>Requisitos

Descarga e instalación de [Herramientas de Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Introducción a U-SQL  

Echemos un vistazo a Hola después script U-SQL:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

Define un conjunto de filas denominado @a y crea un conjunto de filas denominado @results de @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>Expresiones y tipos de C# en un script U-SQL

Una expresión U-SQL es una expresión de C# combinada con operaciones lógicas de U-SQL como `AND`, `OR` y `NOT`. Las expresiones U-SQL pueden utilizarse con SELECT, EXTRACT, WHERE, HAVING, GROUP BY y DECLARE.

Por ejemplo, hello siguiente secuencia de comandos analiza una cadena de un valor de fecha y hora en la cláusula SELECT Hola.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Hello secuencia de comandos siguiente analiza una cadena de un valor de fecha y hora en una instrucción DECLARE.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Uso de expresiones de C# para conversiones de tipo de datos
Hola siguiente ejemplo muestra cómo se puede hacer una conversión de datos de fecha y hora mediante el uso de expresiones de C#. En este escenario en particular, los datos de fecha y hora de cadena están toostandard convertir fecha y hora con la notación de hora de medianoche 00:00:00.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Uso de expresiones de C# para la fecha de hoy
toopull la fecha de hoy, podemos utilizar Hola después de la expresión de C#:

```
DateTime.Now.ToString("M/d/yyyy")
```

Este es un ejemplo de cómo toouse esta expresión en una secuencia de comandos:

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a>Uso de los ensamblados .NET
Modelo de extensibilidad de SQL U depende en gran medida de código personalizado de hello capacidad tooadd. Actualmente, U-SQL proporciona formas sencillas tooadd su propia Microsoft. Código basado en la red (en particular, C#). Sin embargo, también puede agregar código personalizado escrito en otros lenguajes .NET como, por ejemplo, F# o VB.NET. 

### <a name="register-a-net-assembly"></a>Registrar un ensamblado de .NET

Utilice tooplace de instrucción CREATE ASSEMBLY de hello un ensamblado de .NET en una base de datos de SQL U. Una vez que un ensamblado está en una base de datos, scripts U-SQL pueden usar esos ensamblados mediante el uso de la instrucción de ENSAMBLADO de referencia de Hola. 

Hola el siguiente código muestra cómo tooregister un ensamblado:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Hola el siguiente código muestra cómo tooreference un ensamblado:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Consulte hello [instrucciones de registro del ensamblado](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) que tratan en este tema con mayor detalle.


### <a name="use-assembly-versioning"></a>Uso del control de versiones de ensamblado
En la actualidad, SQL U usa Hola .NET Framework versión 4.5. Por tanto, asegúrese de que sus propios ensamblados son compatibles con esa versión de hello en tiempo de ejecución.

Como se mencionó anteriormente, U-SQL ejecuta código en un formato de 64 bits (x64). Asegúrese de que el código está compilado toorun en x64. En caso contrario, obtendrá el error de un formato incorrecto de hello mostrado anteriormente.

El archivo DLL y el de recursos de cada ensamblado cargado como, por ejemplo, un tiempo de ejecución diferente, un ensamblado nativo o un archivo de configuración pueden tener 400 MB como máximo. tamaño total de Hola de recursos implementados, ya sea a través del recurso de implementar o tooassemblies referencias y los archivos adicionales, no puede superar los 3 GB.

Por último, tenga en cuenta que cada base de datos de U-SQL solo puede contener una versión de cualquier ensamblado dado. Por ejemplo, si necesita las versiones 7 y 8 de hello NewtonSoft Json.Net biblioteca, deberá tooregister en dos bases de datos. Además, cada script solo puede hacer referencia tooone versión de un archivo DLL del ensamblado especificado. En este sentido, U-SQL sigue Hola C# ensamblado administración y control de versiones semántica.


## <a name="use-user-defined-functions-udf"></a>Funciones definidas por el usuario: UDF
Funciones definidas por el usuario de SQL U o una UDF, está programando rutinas que aceptan parámetros, realizan una acción (por ejemplo, un cálculo complejo) y devuelven el resultado de hello de esa acción como un valor. Hola devuelve el valor de UDF solo puede ser un valor escalar único. Se puede llamar a UDF de U-SQL en un script base U-SQL como a cualquier otra función escalar de C#.

Es recomendable que inicialice las funciones definidas por el usuario de U-SQL como **públicas** y **estáticas**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Primer Echemos un vistazo a sencillo ejemplo de Hola de creación de una UDF.

En este escenario de caso de uso, necesitamos toodetermine Hola ejercicio, incluyendo trimestre fiscal de Hola y el mes fiscal de hello primer inicio de sesión de usuario específico de Hola. Hola primer mes fiscal del año de hello en nuestro escenario es junio.

toocalculate período fiscal, presentemos Hola después de la función de C#:

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

Simplemente calcula el trimestre y mes fiscal y se devuelve un valor de cadena. En junio, Hola primer mes de hello primer trimestre fiscal, usamos "Q1:P1". Para julio: "Q1:P2" y así sucesivamente.

Se trata de una función de C# normal a que estamos toouse continuo en nuestro proyecto U-SQL.

Este es el aspecto de la sección de código subyacente de hello en este escenario:

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

Ahora vamos toocall esta función desde un script de SQL U base Hola. toodo, tenemos tooprovide un nombre completo para la función hello, incluido el espacio de nombres de hello, que en este caso es NameSpace.Class.Function(parameter).

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Aquí te mostramos Hola real U-base script SQL:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Archivo de salida de hello de ejecución del script de Hola te mostramos:

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

Este ejemplo muestra un uso simple de UDF insertada en U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Mantenimiento del estado entre las invocaciones de UDF
Objetos de programación de C# SQL U pueden ser sofisticados más, utilizando interactividad a través de las variables globales de hello código subyacente. Echemos un vistazo a Hola siguiendo el escenario de caso de uso empresarial.

En organizaciones grandes, los usuarios pueden cambiar entre variedades de aplicaciones internas. Estas pueden incluir Microsoft Dynamics CRM, PowerBI, etc. Los clientes conviene tooapply un análisis de telemetría de cómo los usuarios cambian entre distintas aplicaciones, ¿qué uso Hola tendencias son y así sucesivamente. objetivo de Hello para empresas de hello es toooptimize uso de la aplicación. También es posible que prefiera toocombine distintas aplicaciones o las rutinas de inicio de sesión específicos.

tooachieve este objetivo, tenemos Id. de sesión de toodetermine y el intervalo de tiempo entre Hola última sesión que se ha producido.

Se necesita toofind en un inicio de sesión anterior y, a continuación, asignar este inicio de sesión tooall las sesiones que están siendo toohello generado misma aplicación. primer desafío de Hello es que script de base de U-SQL no nos permitirá tooapply cálculos en columnas calculadas ya con la función LAG. Hello segundo desafío es que tenemos sesión específica de hello tookeep para todas las sesiones en hello mismo período de tiempo.

toosolve este problema, usamos una variable global dentro de una sección de código subyacente: `static public string globalSession;`.

Esta variable global es el conjunto de filas completo toohello aplicada durante la ejecución del script.

Esta es la sección de código subyacente de Hola de nuestro programa U-SQL:

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

En este ejemplo se muestra hello variable global `static public string globalSession;` usa dentro de hello `getStampUserSession` función y la obtención de reinicializan cada sesión se cambia el parámetro hello de tiempo.

Hola script de base de U-SQL es como sigue:

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

Función `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` se denomina aquí durante el cálculo de conjunto de filas de memoria segundo Hola. Pasa hello `UserSessionTimestamp` columna y devuelve Hola valor hasta `UserSessionTimestamp` ha cambiado.

archivo de salida de Hello es como sigue:

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

Este ejemplo muestra un escenario de caso de uso más complicado en la que se utiliza una variable global dentro de una sección de código subyacente que es el conjunto de filas de toohello aplicado toda memoria.

## <a name="use-user-defined-types-udt"></a>Uso de tipos definidos por el usuario: UDT
Los tipos de definidos por el usuario o UDT constituyen otra característica de programación de U-SQL. UDT de U-SQL actúa como un tipo de definido por el usuario de C# normal. C# es un lenguaje fuertemente tipado que permite el uso de Hola de tipos integrados y personalizados definidos por el usuario.

U-SQL implícitamente no se puede serializar o deserializar UDT arbitrarios cuando Hola UDT se pasa entre vértices en conjuntos de filas. Esto significa que el usuario hello tiene tooprovide un formateador explícita mediante Hola IFormatter interfaz. Esto proporciona SQL U con hello serializar y deserializar métodos para hello UDT.

> [!NOTE]
> U-SQL extractores integrados y outputters actualmente no se puede serializar o deserializar UDT tooor de datos de archivos, incluso con hello IFormatter conjunto. Así, cuando escribes tooa archivo de datos UDT con hello instrucción de salida, o que lo lean un extractor de tablas, tendrá que toopass como una cadena o matriz de bytes. A continuación, llama a serialización hello y código (es decir, el método de ToString() Hola UDT) de deserialización explícitamente. Extractores de datos definido por el usuario y outputters en hello otra parte, pueden leer y escribir UDT.

Si se intenta toouse UDT en extractor de tablas o OUTPUTTER (fuera de la selección anterior), como se muestra aquí:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Recibimos Hola siguiente error:

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

toowork con UDT en outputter, ya sea tenemos tooserialize se toostring con Hola método ToString() o crear un outputter personalizado.

Actualmente los UDT no se pueden usar en GROUP BY. Si el UDT se usa GROUP BY, se produce Hola siguiente error:

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

toodefine un UDT, tenemos que:

* Agregue Hola después de los espacios de nombres:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Agregar `Microsoft.Analytics.Interfaces`, lo cual es necesario para las interfaces UDT de Hola. Además, `System.IO` podría ser necesario toodefine Hola IFormatter interfaz.

* Defina un tipo definido por el usuario con el atributo SqlUserDefinedType.

**SqlUserDefinedType** es toomark usa una definición de tipo en un ensamblado como un tipo definido por el usuario (UDT) en SQL U. propiedades de Hello del atributo de hello reflejan sus características físicas de Hola de hello UDT. Esta clase no se puede heredar.

SqlUserDefinedType es un atributo necesario para la definición de UDT.

constructor de Hola de clase hello:  

* SqlUserDefinedTypeAttribute (formateador de tipos)

* Formateador de tipo: requiere un formateador UDT--del parámetro toodefine en concreto, el tipo de Hola de hello `IFormatter` interfaz se debe pasar a continuación.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* UDT típico también requiere la definición de interfaz de IFormatter hello, como se muestra en el siguiente ejemplo de Hola:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Hola `IFormatter` interfaz serializa y deserializa un gráfico de objetos con el tipo de raíz de Hola de \<typeparamref name = "T" >.

\<typeparam nombre = "T" > Hola tipo raíz para tooserialize de gráfico de objeto de Hola y deserializar.

* **Deserializar**: deserializa datos hello en secuencia Hola proporcionado y reconstituye el gráfico de Hola de objetos.

* **Serializar**: serializa un objeto o un gráfico de objetos, con hello dada raíz toohello proporciona secuencia.

`MyType`instancia: instancia de tipo hello.  
`IColumnWriter`sistema de escritura / `IColumnReader` lector: hello secuencia de la columna subyacente.  
`ISerializationContext`contexto: enumeración que define un conjunto de indicadores que especifica el contexto de origen o destino de Hola para hello secuencia durante la serialización.

* **Intermedio**: especifica ese contexto de origen o destino de hello no es un almacén persistente.

* **Persistencia**: especifica ese contexto de origen o destino de hello es un almacén persistente.

Como un tipo de C# normal, la definición de UDT de U-SQL puede incluir invalidaciones para los operadores como +/==/!=. Puede incluir también métodos estáticos. Por ejemplo, si vamos toouse este UDT como una función de agregado MIN de U-SQL de parámetro tooa, tenemos toodefine < invalidación de operador.

Anteriormente en esta guía, se muestra un ejemplo de identificación del período fiscal de fecha específicos de hello en formato de hello Qn:Pn (Q1:P10). Hola de ejemplo siguiente muestra cómo toodefine personalizado escriba para valores del período fiscales.

A continuación aparece un ejemplo de sección de código subyacente con interfaz IFormatter y UDT personalizados:

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

tipo definido Hello incluye dos números: trimestre y mes. Los operadores ==/!=/>/< y el método estático ToString() se definen aquí.

Como se mencionó anteriormente, UDT se puede utilizar en expresiones SELECT, pero no se puede usar en OUTPUTTER/EXTRACTOR sin serialización personalizada. O bien tiene toobe serializado como una cadena con ToString() o usar con un OUTPUTTER/EXTRACTOR personalizado.

Ahora vamos a analizar el uso de UDT. En una sección de código subyacente, hemos cambiado nuestras siguiente de toohello GetFiscalPeriod función:

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

Como puede ver, devuelve el valor de Hola de nuestro tipo FiscalPeriod.

En este caso, proporcionamos un ejemplo de cómo toouse más tarde en el script de base de U-SQL. En este ejemplo se muestran distintas maneras de invocación de UDT a partir del script U-SQL.

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

Este es un ejemplo de una sección de código subyacente completa:

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a>Uso de agregados definidos por el usuario: UDAGG
Los agregados definidos por el usuario son todas las funciones relacionadas con la agregación que no se distribuyen de fábrica con U-SQL. ejemplo de Hola puede ser un agregado tooperform cálculos matemáticas personalizadas, concatenaciones de cadenas, manipulaciones de cadenas y así sucesivamente.

definición de clase de base agregado definido por el usuario de Hello es como sigue:

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

**SqlUserDefinedAggregate** indica que el tipo de hello debe registrarse como un agregado definido por el usuario. Esta clase no se puede heredar.

El atributo SqlUserDefinedType es **opcional** para la definición de UDAGG.


Hello clase base permite parámetros abstracta toopass tres: dos como parámetros de entrada y uno de ellos como resultado de hello. tipos de datos de Hello son variables y deben definirse durante la herencia de clases.

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* **Init** se invoca una vez para cada grupo durante el cálculo. Proporciona la rutina de inicialización para cada grupo de agregación.  
* **Accumulate** se ejecuta una vez para cada valor. Proporciona funcionalidad principal de hello para el algoritmo de agregación de Hola. Puede ser valores tooaggregate usadas con diversos tipos de datos que se definen durante la herencia de clases. Puede aceptar dos parámetros de tipos de datos de variable.
* **Terminar** se ejecuta una vez por cada grupo de agregación final Hola del resultado de hello toooutput para cada grupo de procesamiento.

entrada correcta toodeclare y tipos de datos de salida, use definición de clase de hello como sigue:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: Primer parámetro tooaccumulate
* T2: Primer parámetro tooaccumulate
* TResult: Tipo de valor devuelto de Terminate

Por ejemplo:

```
public class GuidAggregate : IAggregate<string, int, int>
```

o

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Uso de UDAGG en U-SQL
toouse UDAGG, primero defina en el código subyacente o referencia a ella desde la programación existente de hello DLL como se indicó anteriormente.

A continuación, usar hello según la sintaxis:

```
AGG<UDAGG_functionname>(param1,param2)
```

A continuación se muestra un ejemplo de UDAGG:

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

Y el script base U-SQL:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

En este escenario de caso de uso, se concatena clase GUID para usuarios específicos de Hola.

## <a name="use-user-defined-objects-udo"></a>Uso de objetos definidos por el usuario: UDO
U-SQL permite objetos de programación personalizado toodefine, que se denominan objetos definidos por el usuario o UDO.

Hola mostramos una lista de UDO en U-SQL:

* Extractores definidos por el usuario
    * Extraer fila por fila
    * Utilizar extracción de datos de tooimplement desde archivos estructurados personalizados

* Outputters definidos por el usuario
    * Dar salida fila por fila
    * Utilizar tipos de datos personalizados de toooutput o formatos de archivo personalizados

* Procesadores definidos por el usuario
    * Tomar una fila y producir una fila
    * Tooreduce usado Hola número de columnas o generar nuevas columnas con valores que se derivan de una columna existente

* Aplicadores definidos por el usuario
    * Tomar una fila y generar 0 filas toon
    * Se usa con CROSS/OUTER APPLY

* Combinadores definidos por el usuario
    * Combina conjuntos de filas (JOIN definidas por el usuario)

* Reductores definidos por el usuario
    * Tomar n filas y producir una fila
    * Usar tooreduce Hola un número de filas

UDO se suele llamar explícitamente en el script U-SQL como parte del programa Hola siguiendo las instrucciones SQL U:

* EXTRACT
* OUTPUT
* PROCESS
* COMBINE
* REDUCE

> [!NOTE]  
> UDO es 0,5 Gb de memoria de tooconsume limitado.  Esta limitación de memoria no aplica a las ejecuciones de toolocal.

## <a name="use-user-defined-extractors"></a>Uso de extractores definidos por el usuario
U-SQL permite tooimport de datos externos mediante una instrucción de extracción. La instrucción EXTRACT puede utilizar extractores UDO integrados:  

* *Extractors.Text()*: Proporciona extracción de archivos de texto delimitado de diferentes codificaciones.

* *Extractors.Csv()*: Proporciona extracción de archivos de valores separados por comas (CSV) de diferentes codificaciones.

* *Extractors.Tsv()*: Proporciona extracción de archivos de valores separados por tabulaciones (TSV) de diferentes codificaciones.

Puede ser útil toodevelop un extractor de datos personalizado. Esto puede resultar útil durante la importación de datos si queremos toodo cualquiera de hello siguientes tareas:

* Modificar datos de entrada mediante la división de columnas y modificar valores individuales. Hola funcionalidad del procesador es mejor para combinar las columnas.
* Analizar datos no estructurados, como páginas web o correos electrónicos o datos parcialmente no estructurados, como XML o JSON.
* Analizar datos en codificación no compatible.

toodefine extractor de tablas definidas por el usuario, o uir, tenemos toocreate un `IExtractor` interfaz. Todos los extractor de tablas de parámetros toohello, de entrada, como delimitadores de columna o fila y la codificación, deben toobe definido en hello constructor de clase hello. Hola `IExtractor` interfaz también debe contener una definición de hello `IEnumerable<IRow>` invalidar como sigue:

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

Hola **SqlUserDefinedExtractor** atributo indica que el tipo de hello debe registrarse como un extractor de tablas definidas por el usuario. Esta clase no se puede heredar.

SqlUserDefinedExtractor es un atributo opcional para la definición de UDE. Utiliza toodefine AtomicFileProcessing propiedad para el objeto de uir Hola.

* bool     AtomicFileProcessing   

* **true** = Indica que este extractor requiere archivos de entrada atómicos (JSON, XML...)
* **false** = Indica que este extractor puede tratar con archivos divididos o distribuidos (CSV, SEQ...)

objetos de programación de Hello principales uir son **entrada** y **salida**. objeto de entrada de Hello es tooenumerate usa datos de entrada como `IUnstructuredReader`. objeto de salida de Hello es tooset usa datos de salida como resultado de la actividad de hello extractor de tablas.

se tiene acceso a datos de entrada de Hola a través de `System.IO.Stream` y `System.IO.StreamReader`.

Para la enumeración de las columnas de entrada, en primer lugar dividiremos flujo de entrada de hello utilizando un delimitador de filas.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Después, dividiremos aún más la fila de entrada en partes de la columna.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

tooset los datos de salida, usaremos hello `output.Set` método.

Es importante toounderstand que Hola extractor personalizado genera solo las columnas y los valores que se definen con salida de hello. Establezca la llamada del método.

```
output.Set<string>(count, part);
```

salida de Hello extractor reales se desencadena mediante una llamada a `yield return output.AsReadOnly();`.

Aquí te mostramos hello (ejemplo) extractor de tablas:

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

En este escenario de caso de uso, extractor de Hola Hola GUID para la columna "guid", vuelve a generar y convierte los valores de hello de caso de tooupper de columna de "usuario". Los extractores personalizados pueden producir resultados más complicados mediante el análisis de datos de entrada y la manipulación de estos.

Este es un script base U-SQL que utiliza un extractor personalizado:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a>Uso de outputters definidos por el usuario
Outputter definido por el usuario es UDO SQL U otro que permite la funcionalidad integrada de U-SQL de tooextend. Extractor de tablas toohello similar, hay varios outputters integrados.

* *Outputters.Text()*: escribe datos toodelimited archivos de texto de diferentes codificaciones.
* *Outputters.Csv()*: escribe datos toocomma de valores separados archivos (CSV) de diferentes codificaciones.
* *Outputters.Tsv()*: escribe datos tootab de valores separados archivos (TSV) de diferentes codificaciones.

Outputter personalizado permite toowrite datos en un formato personalizado definido. Esto puede ser útil para hello siguientes tareas:

* Escribir archivos de datos de toosemi estructurados o no estructurados.
* Escribir datos en codificaciones no admitidas.
* Modificar datos de salida o agregar atributos personalizados.

toodefine definido por el usuario outputter, necesitamos hello toocreate `IOutputter` interfaz.

Aquí te mostramos Hola base `IOutputter` la implementación de clase:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Todos los parámetros toohello outputter, de entrada, como delimitadores de columna o fila, la codificación y así sucesivamente, deben toobe definido en hello constructor de clase hello. Hola `IOutputter` interfaz también debe contener una definición para `void Output` invalidar. atributo de Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` , opcionalmente, se puede establecer para el procesamiento de archivos atómica. Para obtener más información, vea Hola detalles siguientes.

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* `Output` se llama para cada fila de entrada. Devuelve hello `IUnstructuredWriter output` conjunto de filas.
* se utiliza Hola clase del Constructor definido por el usuario outputter de toopass parámetros toohello.
* `Close`se utiliza toooptionally invalidar toorelease costoso estado o para determinar cuándo se escribió la última fila de Hola.

**SqlUserDefinedOutputter** atributo indica que el tipo de hello debe registrarse como un outputter definido por el usuario. Esta clase no se puede heredar.

SqlUserDefinedOutputter es un atributo opcional para la definición del outputter definido por el usuario. Ha utilizado la propiedad AtomicFileProcessing de toodefine Hola.

* bool     AtomicFileProcessing   

* **true** = Indica que este outputter requiere archivos de salida atómicos (JSON, XML...)
* **false** = Indica que este outputter puede tratar con archivos divididos o distribuidos (CSV, SEQ...)

los objetos de programación principal Hola son **fila** y **salida**. Hola **fila** objeto es tooenumerate usa datos de salida como `IRow` interfaz. **Salida** es archivo de destino de toohello de datos de salida de tooset usado.

Hello datos de salida se tiene acceso a través de hello `IRow` interfaz. Los datos de salida pasan una fila en cada momento.

se enumeran los valores individuales de Hello llamando al método Get hello de interfaz IRow de hello:

```
row.Get<string>("column_name")
```

Los nombres de columna individuales se pueden determinar mediante una llamada a `row.Schema`:

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Este enfoque permite toobuild un outputter flexible para cualquier esquema de metadatos.

Hello datos de salida se escriben toofile utilizando `System.IO.StreamWriter`. parámetro de la secuencia de Hola se establece demasiado`output.BaseStrea` como parte de `IUnstructuredWriter output`.

Tenga en cuenta que es importante tooflush Hola datos búfer toohello archivo después de cada iteración de la fila. Además, Hola `StreamWriter` objeto debe utilizarse con hello descartables atributo habilitado (valor predeterminado) y con hello **con** palabra clave:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

De lo contrario, llame al método Flush() explícitamente después de cada iteración. Esto se muestra en el siguiente ejemplo de Hola.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Establecimiento de encabezados y pies de página para el outputter definido por el usuario
tooset un encabezado, use el flujo de ejecución de la iteración.

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

Hola código de hello primero `if (isHeaderRow)` bloque se ejecuta solo una vez.

Pie de página de hello, usar la instancia de toohello de referencia de Hola de `System.IO.Stream` objeto (`output.BaseStream`). Escribir el pie de página de Hola Hola método Close() de hello `IOutputter` interfaz.  (Para obtener más información, vea la siguiente ejemplo de Hola.)

Este es un ejemplo de un outputter definido por el usuario:

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

Y el script base U-SQL:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

Se trata de un outputter HTML que crea un archivo HTML con los datos de la tabla.

### <a name="call-outputter-from-u-sql-base-script"></a>Llamada a un outputter desde el script base U-SQL
toocall un outputter personalizado desde un script de SQL U base hello, Hola nueva instancia del objeto de hello outputter tiene toobe creado.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

tooavoid crear una instancia del programa Hola a objeto en un script de base, podemos crear un contenedor de la función, como se muestra en el ejemplo anterior:

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

En este caso, llamada original Hola Hola siguiente aspecto:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Uso de procesadores definidos por el usuario
Procesador definido por el usuario o UDP, es un tipo de UDO U-SQL que permite las filas entrantes tooprocess Hola aplicando características de programación. UDP permite toocombine columnas, modifique los valores y agregar nuevas columnas si es necesario. Básicamente, ayuda a tooprocess unos elementos de datos de conjunto de filas tooproduce necesario.

toodefine un UDP, necesitamos toocreate una `IProcessor` interfaz con hello `SqlUserDefinedProcessor` atributo, que es opcional para UDP.

Esta interfaz debe contener la definición de Hola para hello `IRow` invalidar el conjunto de filas de interfaz, como se muestra en el siguiente ejemplo de Hola:

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

**SqlUserDefinedProcessor** indica que el tipo de hello debe registrarse como un procesador definido por el usuario. Esta clase no se puede heredar.

atributo de Hello SqlUserDefinedProcessor es **opcional** para la definición de UDP.

los objetos de programación principal Hola son **entrada** y **salida**. objeto de entrada de Hello es tooenumerate usa las columnas de entrada y salida y datos de salida de tooset como resultado de la actividad del procesador Hola.

Para la enumeración de las columnas de entrada, usamos hello `input.Get` método.

```
string column_name = input.Get<string>("column_name");
```

Hola parámetro `input.Get` método es una columna que se pasa como parte del programa Hola a `PRODUCE` cláusula de hello `PROCESS` instrucción de script de base de hello U-SQL. Necesitamos toouse datos correctos de hello escriba aquí.

Para la salida, usar hello `output.Set` método.

Es importante toonote ese productor personalizado solo genera columnas y valores que se definen con hello `output.Set` llamada al método.

```
output.Set<string>("mycolumn", mycolumn);
```

salida de Hello real del procesador se activa mediante una llamada a `return output.AsReadOnly();`.

Este es un ejemplo de procesador:

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

En este escenario de caso de uso, el procesador de hello está generando una nueva columna denominada "full_description" mediante la combinación de hello las columnas existentes: en este caso, "usuario" en mayúsculas y "des". También se vuelve a generar un GUID y se devuelve Hola originales y los nuevos valores GUID.

Como puede ver de ejemplo de Hola a anterior, puede llamar a métodos de C# durante `output.Set` llamada al método.

Este es un ejemplo de script U-SQL base que utiliza un procesador personalizado:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a>Uso de aplicadores definidos por el usuario
Un aplicador de U-SQL definido por el usuario permite función tooinvoke personalizado C# para cada fila devuelta por la expresión de tabla externa de Hola de una consulta. Hola de entrada derecha se evalúa para cada fila de entrada izquierda hello y filas de hello producidas se combinan para la salida final Hola. Hola lista de columnas que se producen por el operador APPLY de Hola son la combinación de Hola de conjunto de Hola de columnas de la izquierda de Hola y Hola de entrada derecha.

Se está llamando a aplicador definido por el usuario como parte del programa Hola USQL seleccione expresión.

Hola llamada típica toohello definido por el usuario aplicador parece Hola siguiente:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Consulte [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (U-SQL SELECT, selección de CROSS APPLY y OUTER APPLY) para más información sobre cómo utilizar aplicadores en una expresión SELECT.

definición de clase base aplicador de Hello definido por el usuario es como sigue:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine un aplicador definido por el usuario, necesitamos hello toocreate `IApplier` interfaz con hello [`SqlUserDefinedApplier`] atributo, que es opcional para una definición de aplicador definido por el usuario.

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* Aplicar se llama para cada fila de tabla externa Hola. Devuelve hello `IUpdatableRow` conjunto de filas de salida.
* clase de Constructor Hello es toopass usa parámetros toohello definido por el usuario aplicador.

**SqlUserDefinedApplier** indica que el tipo de hello debe registrarse como un aplicador definido por el usuario. Esta clase no se puede heredar.

**SqlUserDefinedApplier** es **opcional** para la definición del aplicador definido por el usuario.


objetos de programación principales de Hello son los siguientes:

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Los conjuntos de filas de entrada se pasan como entrada `IRow`. Hello salida se generan filas como `IUpdatableRow` interfaz de salida.

Nombres de columna individuales se pueden determinar mediante llamada hello `IRow` método de esquema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

valores de datos reales de hello tooget de Hola entrante `IRow`, usamos hello Get() método `IRow` interfaz.

```
mycolumn = row.Get<int>("mycolumn")
```

O bien, se utiliza el nombre de columna del esquema de hello:

```
row.Get<int>(row.Schema[0].Name)
```

Hello valores de salida deben establecerse con `IUpdatableRow` salida:

```
output.Set<int>("mycolumn", mycolumn)
```

Es importante toounderstand que aplicadores personalizados sólo genera resultados columnas y valores que se definen con `output.Set` llamada al método.

salida real de Hola se desencadena mediante una llamada a `yield return output.AsReadOnly();`.

se pueden pasar parámetros aplicador de Hello definidos por el usuario toohello constructor. Aplicador de puede devolver un número variable de columnas que deben toobe definido durante la llamada aplicador de hello en el Script U-SQL base.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Este es ejemplo aplicador de hello definido por el usuario:

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

Aquí te mostramos Hola base U-secuencia de comandos SQL para este aplicador definido por el usuario:

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

En este escenario de caso de uso, definido por el usuario aplicador actúa como un analizador de valores delimitados por comas para automóvil Hola flota propiedades. filas del archivo de entrada de Hello aspecto Hola siguiente:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Es un archivo TSV delimitado por tabulaciones típico con la columna de propiedades que contiene las propiedades de los automóviles, como la marca y el modelo. Esas propiedades deben ser columnas de la tabla de toohello analizado. aplicador de Hola que se proporciona también le permite toogenerate conjunto de filas, en función de hello parámetro que se pasa como resultado un número de propiedades en hello dinámico. Puede generar todas las propiedades o solo un conjunto específico de propiedades.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

aplicador de Hello definido por el usuario se pueda llamar como una nueva instancia de objeto aplicador:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

O con la invocación de Hola de un método de fábrica de contenedor:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Uso de combinadores definidos por el usuario
Combinador definido por el usuario, o UDC, le permite toocombine filas de conjuntos de filas izquierdo y derecho, en función de la lógica personalizada. El combinador definido por el usuario se utiliza con la expresión de COMBINE.

Se está llamando a un Combinador con expresión de combinación de Hola que proporciona Hola información necesaria sobre ambos conjuntos de filas de entrada de hello, Hola agrupación de columnas, hello espera esquema resultados e información adicional.

toocall un Combinador en un script U-SQL base, utilizamos Hola según la sintaxis:

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

Para más información, vea [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx) (Expresión COMBINE (U-SQL)).

toodefine un Combinador definido por el usuario, necesitamos hello toocreate `ICombiner` interfaz con hello [`SqlUserDefinedCombiner`] atributo, que es opcional para una definición de Combinador definido por el usuario.

Definición de clase base `ICombiner`:

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

Hola implementación personalizada de un `ICombiner` interfaz debe contener la definición de Hola para un `IEnumerable<IRow>` combinar invalidación.

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

Hola **SqlUserDefinedCombiner** atributo indica que el tipo de hello debe registrarse como un Combinador definido por el usuario. Esta clase no se puede heredar.

**SqlUserDefinedCombiner** es propiedad de modo de Combinador de hello toodefine usado. Es un atributo opcional para la definición de un combinador definido por el usuario.

Modo CombinerMode

Enumeración CombinerMode puede tomar Hola siguientes valores:

* Completo (0), de que cada fila de resultados depende potencialmente de todas las filas de entrada de Hola izquierda y derecha con hello mismo valor de clave.

* Izquierda (1), cada fila de salida depende de una sola fila de entrada de hello izquierda (y potencialmente todas las filas de hello derecha con hello mismo valor de clave).

* Derecha (2), cada fila de salida depende de una sola fila de entrada de hello derecho (y potencialmente todas las filas de hello izquierda con hello mismo valor de clave).

* Interna (3), cada fila de salida depende de una sola entrada de fila de la izquierda y derecha con hello igual valor.

Ejemplo:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


objetos de programación principal Hola son:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Los conjuntos de filas de entrada se pasan como el tipo de interfaz `IRowset` **left** y **right**. Ambos conjuntos de filas deben enumerarse para su procesamiento. Sólo puede enumerar cada interfaz una vez, por lo que tiene tooenumerate y almacenarla en la caché si es necesario.

Para el almacenamiento en caché, se puede crear un tipo de estructura de memoria List\<T\> como resultado de la ejecución de la consulta LINQ y, más concretamente, List<`IRow`>. tipo de datos anónimos Hola puede usarse durante la enumeración también.

Vea [Introducción tooLINQ consultas (C#)](https://msdn.microsoft.com/library/bb397906.aspx) para obtener más información acerca de las consultas LINQ, y [IEnumerable\<T\> interfaz](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) para obtener más información acerca de IEnumerable\<T\> interfaz.

valores de datos reales de hello tooget de Hola entrante `IRowset`, usamos hello Get() método `IRow` interfaz.

```
mycolumn = row.Get<int>("mycolumn")
```

Nombres de columna individuales se pueden determinar mediante llamada hello `IRow` método de esquema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

O mediante el nombre de columna del esquema de hello:

```
c# row.Get<int>(row.Schema[0].Name)
```

enumeración general de Hello con LINQ es similar a Hola siguiente:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

Después de enumerar los conjuntos de filas, vamos tooloop a través de todas las filas. Para cada fila de conjunto de filas izquierdo hello, vamos toofind todas las filas que cumplen la condición de Hola de nuestro Combinador.

Hello valores de salida deben establecerse con `IUpdatableRow` salida.

```
output.Set<int>("mycolumn", mycolumn)
```

salida real de Hola se desencadena mediante una llamada a demasiado`yield return output.AsReadOnly();`.

Este es un ejemplo de combinador:

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

En este escenario de caso de uso, estamos creando un informe de análisis para el distribuidor de Hola. objetivo de Hello es toofind todos los productos cuyo costo es más de 20.000 USD y que se venden a través del sitio Web de hello más rápido que a través de distribuidor regular de hello dentro de un período de tiempo determinado.

Este es el script U-SQL base de Hola. Puede comparar la lógica de hello entre una combinación normal y un Combinador:

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

Un Combinador definido por el usuario se pueda llamar como una nueva instancia de objeto aplicador de hello:

```
USING new MyNameSpace.MyCombiner();
```


O con la invocación de Hola de un método de fábrica de contenedor:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Uso de reductores definidos por el usuario

U-SQL permite toowrite reductores de conjunto de filas personalizadas en C# con marco de extensibilidad de hello operador definido por el usuario e implementando una interfaz IReducer.

Reductor definido por el usuario, o UDR, puede ser las filas innecesarias tooeliminate usado durante la extracción de datos (importar). También puede ser usado toomanipulate y evaluar las filas y columnas. En función de la lógica de programación, también puede definir qué filas necesitan toobe extraído.

una clase UDR toodefine, necesitamos toocreate una `IReducer` interfaz con una función opcional `SqlUserDefinedReducer` atributo.

Esta interfaz de clase debe contener una definición de hello `IEnumerable` invalidar el conjunto de filas de interfaz.

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

Hola **SqlUserDefinedReducer** atributo indica que el tipo de hello debe registrarse como un reductor definido por el usuario. Esta clase no se puede heredar.
**SqlUserDefinedReducer** es un atributo opcional para la definición del reductor definido por el usuario. Ha utilizado toodefine IsRecursive propiedad.

* bool     IsRecursive    
* **true**  = Indica si el reductor es idempotente

los objetos de programación principal Hola son **entrada** y **salida**. objeto de entrada de Hello es tooenumerate usado filas de entrada. Salida es tooset usado filas de salida como resultado de la reducción de actividad.

Para la enumeración de filas de entrada, usamos hello `Row.Get` método.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

Hola parámetro hello `Row.Get` método es una columna que se pasa como parte del programa Hola a `PRODUCE` clase de hello `REDUCE` instrucción de script de base de hello U-SQL. Necesitamos toouse Hola tipo de datos correcto aquí también.

Para la salida, usar hello `output.Set` método.

Es importante toounderstand que valores salidas solo reductor personalizados que se definen con Hola `output.Set` llamada al método.

```
output.Set<string>("mycolumn", guid);
```

salida de Hello reductor reales se desencadena mediante una llamada a `yield return output.AsReadOnly();`.

Este es un ejemplo de reductor:

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

En este escenario de caso de uso, omite el reductor Hola filas con un nombre de usuario vacío. Para cada fila de conjunto de filas, lee cada columna necesaria y después se evalúa como longitud de Hola Hola del nombre de usuario. Produce el resultado real de la fila Hola solo si la longitud del valor de nombre de usuario es mayor que 0.

Este es un script base U-SQL que utiliza un reductor personalizado:

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
