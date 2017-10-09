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
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="ee53b-103">Guía de programación de U-SQL</span><span class="sxs-lookup"><span data-stu-id="ee53b-103">U-SQL programmability guide</span></span>

<span data-ttu-id="ee53b-104">U-SQL es un lenguaje de consulta diseñado para tipo de macrodatos de cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ee53b-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="ee53b-105">Una de las características únicas de Hola de U-SQL es la combinación de Hola de lenguaje declarativo de hello similar a SQL con la extensibilidad de Hola y capacidad de programación que se proporciona en C#.</span><span class="sxs-lookup"><span data-stu-id="ee53b-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="ee53b-106">En esta guía, se concentrarse en la extensibilidad de Hola y capacidad de programación del lenguaje de U-SQL de Hola que está habilitada en C#.</span><span class="sxs-lookup"><span data-stu-id="ee53b-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="ee53b-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="ee53b-107">Requirements</span></span>

<span data-ttu-id="ee53b-108">Descarga e instalación de [Herramientas de Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="ee53b-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="ee53b-109">Introducción a U-SQL</span><span class="sxs-lookup"><span data-stu-id="ee53b-109">Get started with U-SQL</span></span>  

<span data-ttu-id="ee53b-110">Echemos un vistazo a Hola después script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="ee53b-110">Let’s look at hello following U-SQL script:</span></span>

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

<span data-ttu-id="ee53b-111">Define un conjunto de filas denominado @a y crea un conjunto de filas denominado @results de @a.</span><span class="sxs-lookup"><span data-stu-id="ee53b-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="ee53b-112">Expresiones y tipos de C# en un script U-SQL</span><span class="sxs-lookup"><span data-stu-id="ee53b-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="ee53b-113">Una expresión U-SQL es una expresión de C# combinada con operaciones lógicas de U-SQL como `AND`, `OR` y `NOT`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="ee53b-114">Las expresiones U-SQL pueden utilizarse con SELECT, EXTRACT, WHERE, HAVING, GROUP BY y DECLARE.</span><span class="sxs-lookup"><span data-stu-id="ee53b-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="ee53b-115">Por ejemplo, hello siguiente secuencia de comandos analiza una cadena de un valor de fecha y hora en la cláusula SELECT Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="ee53b-116">Hello secuencia de comandos siguiente analiza una cadena de un valor de fecha y hora en una instrucción DECLARE.</span><span class="sxs-lookup"><span data-stu-id="ee53b-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="ee53b-117">Uso de expresiones de C# para conversiones de tipo de datos</span><span class="sxs-lookup"><span data-stu-id="ee53b-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="ee53b-118">Hola siguiente ejemplo muestra cómo se puede hacer una conversión de datos de fecha y hora mediante el uso de expresiones de C#.</span><span class="sxs-lookup"><span data-stu-id="ee53b-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="ee53b-119">En este escenario en particular, los datos de fecha y hora de cadena están toostandard convertir fecha y hora con la notación de hora de medianoche 00:00:00.</span><span class="sxs-lookup"><span data-stu-id="ee53b-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="ee53b-120">Uso de expresiones de C# para la fecha de hoy</span><span class="sxs-lookup"><span data-stu-id="ee53b-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="ee53b-121">toopull la fecha de hoy, podemos utilizar Hola después de la expresión de C#:</span><span class="sxs-lookup"><span data-stu-id="ee53b-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="ee53b-122">Este es un ejemplo de cómo toouse esta expresión en una secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="ee53b-122">Here's an example of how toouse this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="ee53b-123">Uso de los ensamblados .NET</span><span class="sxs-lookup"><span data-stu-id="ee53b-123">Using .NET assemblies</span></span>
<span data-ttu-id="ee53b-124">Modelo de extensibilidad de SQL U depende en gran medida de código personalizado de hello capacidad tooadd.</span><span class="sxs-lookup"><span data-stu-id="ee53b-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="ee53b-125">Actualmente, U-SQL proporciona formas sencillas tooadd su propia Microsoft. Código basado en la red (en particular, C#).</span><span class="sxs-lookup"><span data-stu-id="ee53b-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="ee53b-126">Sin embargo, también puede agregar código personalizado escrito en otros lenguajes .NET como, por ejemplo, F# o VB.NET.</span><span class="sxs-lookup"><span data-stu-id="ee53b-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="ee53b-127">Registrar un ensamblado de .NET</span><span class="sxs-lookup"><span data-stu-id="ee53b-127">Register a .NET assembly</span></span>

<span data-ttu-id="ee53b-128">Utilice tooplace de instrucción CREATE ASSEMBLY de hello un ensamblado de .NET en una base de datos de SQL U.</span><span class="sxs-lookup"><span data-stu-id="ee53b-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="ee53b-129">Una vez que un ensamblado está en una base de datos, scripts U-SQL pueden usar esos ensamblados mediante el uso de la instrucción de ENSAMBLADO de referencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="ee53b-130">Hola el siguiente código muestra cómo tooregister un ensamblado:</span><span class="sxs-lookup"><span data-stu-id="ee53b-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="ee53b-131">Hola el siguiente código muestra cómo tooreference un ensamblado:</span><span class="sxs-lookup"><span data-stu-id="ee53b-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="ee53b-132">Consulte hello [instrucciones de registro del ensamblado](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) que tratan en este tema con mayor detalle.</span><span class="sxs-lookup"><span data-stu-id="ee53b-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="ee53b-133">Uso del control de versiones de ensamblado</span><span class="sxs-lookup"><span data-stu-id="ee53b-133">Use assembly versioning</span></span>
<span data-ttu-id="ee53b-134">En la actualidad, SQL U usa Hola .NET Framework versión 4.5.</span><span class="sxs-lookup"><span data-stu-id="ee53b-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="ee53b-135">Por tanto, asegúrese de que sus propios ensamblados son compatibles con esa versión de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="ee53b-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="ee53b-136">Como se mencionó anteriormente, U-SQL ejecuta código en un formato de 64 bits (x64).</span><span class="sxs-lookup"><span data-stu-id="ee53b-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="ee53b-137">Asegúrese de que el código está compilado toorun en x64.</span><span class="sxs-lookup"><span data-stu-id="ee53b-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="ee53b-138">En caso contrario, obtendrá el error de un formato incorrecto de hello mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="ee53b-139">El archivo DLL y el de recursos de cada ensamblado cargado como, por ejemplo, un tiempo de ejecución diferente, un ensamblado nativo o un archivo de configuración pueden tener 400 MB como máximo.</span><span class="sxs-lookup"><span data-stu-id="ee53b-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="ee53b-140">tamaño total de Hola de recursos implementados, ya sea a través del recurso de implementar o tooassemblies referencias y los archivos adicionales, no puede superar los 3 GB.</span><span class="sxs-lookup"><span data-stu-id="ee53b-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="ee53b-141">Por último, tenga en cuenta que cada base de datos de U-SQL solo puede contener una versión de cualquier ensamblado dado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="ee53b-142">Por ejemplo, si necesita las versiones 7 y 8 de hello NewtonSoft Json.Net biblioteca, deberá tooregister en dos bases de datos.</span><span class="sxs-lookup"><span data-stu-id="ee53b-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="ee53b-143">Además, cada script solo puede hacer referencia tooone versión de un archivo DLL del ensamblado especificado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="ee53b-144">En este sentido, U-SQL sigue Hola C# ensamblado administración y control de versiones semántica.</span><span class="sxs-lookup"><span data-stu-id="ee53b-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="ee53b-145">Funciones definidas por el usuario: UDF</span><span class="sxs-lookup"><span data-stu-id="ee53b-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="ee53b-146">Funciones definidas por el usuario de SQL U o una UDF, está programando rutinas que aceptan parámetros, realizan una acción (por ejemplo, un cálculo complejo) y devuelven el resultado de hello de esa acción como un valor.</span><span class="sxs-lookup"><span data-stu-id="ee53b-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="ee53b-147">Hola devuelve el valor de UDF solo puede ser un valor escalar único.</span><span class="sxs-lookup"><span data-stu-id="ee53b-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="ee53b-148">Se puede llamar a UDF de U-SQL en un script base U-SQL como a cualquier otra función escalar de C#.</span><span class="sxs-lookup"><span data-stu-id="ee53b-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="ee53b-149">Es recomendable que inicialice las funciones definidas por el usuario de U-SQL como **públicas** y **estáticas**.</span><span class="sxs-lookup"><span data-stu-id="ee53b-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="ee53b-150">Primer Echemos un vistazo a sencillo ejemplo de Hola de creación de una UDF.</span><span class="sxs-lookup"><span data-stu-id="ee53b-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="ee53b-151">En este escenario de caso de uso, necesitamos toodetermine Hola ejercicio, incluyendo trimestre fiscal de Hola y el mes fiscal de hello primer inicio de sesión de usuario específico de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="ee53b-152">Hola primer mes fiscal del año de hello en nuestro escenario es junio.</span><span class="sxs-lookup"><span data-stu-id="ee53b-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="ee53b-153">toocalculate período fiscal, presentemos Hola después de la función de C#:</span><span class="sxs-lookup"><span data-stu-id="ee53b-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

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

<span data-ttu-id="ee53b-154">Simplemente calcula el trimestre y mes fiscal y se devuelve un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="ee53b-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="ee53b-155">En junio, Hola primer mes de hello primer trimestre fiscal, usamos "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="ee53b-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="ee53b-156">Para julio: "Q1:P2" y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="ee53b-157">Se trata de una función de C# normal a que estamos toouse continuo en nuestro proyecto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="ee53b-158">Este es el aspecto de la sección de código subyacente de hello en este escenario:</span><span class="sxs-lookup"><span data-stu-id="ee53b-158">Here is how hello code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="ee53b-159">Ahora vamos toocall esta función desde un script de SQL U base Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="ee53b-160">toodo, tenemos tooprovide un nombre completo para la función hello, incluido el espacio de nombres de hello, que en este caso es NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="ee53b-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="ee53b-161">Aquí te mostramos Hola real U-base script SQL:</span><span class="sxs-lookup"><span data-stu-id="ee53b-161">Following is hello actual U-SQL base script:</span></span>

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

<span data-ttu-id="ee53b-162">Archivo de salida de hello de ejecución del script de Hola te mostramos:</span><span class="sxs-lookup"><span data-stu-id="ee53b-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="ee53b-163">Este ejemplo muestra un uso simple de UDF insertada en U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="ee53b-164">Mantenimiento del estado entre las invocaciones de UDF</span><span class="sxs-lookup"><span data-stu-id="ee53b-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="ee53b-165">Objetos de programación de C# SQL U pueden ser sofisticados más, utilizando interactividad a través de las variables globales de hello código subyacente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="ee53b-166">Echemos un vistazo a Hola siguiendo el escenario de caso de uso empresarial.</span><span class="sxs-lookup"><span data-stu-id="ee53b-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="ee53b-167">En organizaciones grandes, los usuarios pueden cambiar entre variedades de aplicaciones internas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="ee53b-168">Estas pueden incluir Microsoft Dynamics CRM, PowerBI, etc.</span><span class="sxs-lookup"><span data-stu-id="ee53b-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="ee53b-169">Los clientes conviene tooapply un análisis de telemetría de cómo los usuarios cambian entre distintas aplicaciones, ¿qué uso Hola tendencias son y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="ee53b-170">objetivo de Hello para empresas de hello es toooptimize uso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ee53b-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="ee53b-171">También es posible que prefiera toocombine distintas aplicaciones o las rutinas de inicio de sesión específicos.</span><span class="sxs-lookup"><span data-stu-id="ee53b-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="ee53b-172">tooachieve este objetivo, tenemos Id. de sesión de toodetermine y el intervalo de tiempo entre Hola última sesión que se ha producido.</span><span class="sxs-lookup"><span data-stu-id="ee53b-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="ee53b-173">Se necesita toofind en un inicio de sesión anterior y, a continuación, asignar este inicio de sesión tooall las sesiones que están siendo toohello generado misma aplicación.</span><span class="sxs-lookup"><span data-stu-id="ee53b-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="ee53b-174">primer desafío de Hello es que script de base de U-SQL no nos permitirá tooapply cálculos en columnas calculadas ya con la función LAG.</span><span class="sxs-lookup"><span data-stu-id="ee53b-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="ee53b-175">Hello segundo desafío es que tenemos sesión específica de hello tookeep para todas las sesiones en hello mismo período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="ee53b-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="ee53b-176">toosolve este problema, usamos una variable global dentro de una sección de código subyacente: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="ee53b-177">Esta variable global es el conjunto de filas completo toohello aplicada durante la ejecución del script.</span><span class="sxs-lookup"><span data-stu-id="ee53b-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="ee53b-178">Esta es la sección de código subyacente de Hola de nuestro programa U-SQL:</span><span class="sxs-lookup"><span data-stu-id="ee53b-178">Here is hello code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="ee53b-179">En este ejemplo se muestra hello variable global `static public string globalSession;` usa dentro de hello `getStampUserSession` función y la obtención de reinicializan cada sesión se cambia el parámetro hello de tiempo.</span><span class="sxs-lookup"><span data-stu-id="ee53b-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="ee53b-180">Hola script de base de U-SQL es como sigue:</span><span class="sxs-lookup"><span data-stu-id="ee53b-180">hello U-SQL base script is as follows:</span></span>

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

<span data-ttu-id="ee53b-181">Función `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` se denomina aquí durante el cálculo de conjunto de filas de memoria segundo Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="ee53b-182">Pasa hello `UserSessionTimestamp` columna y devuelve Hola valor hasta `UserSessionTimestamp` ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="ee53b-183">archivo de salida de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="ee53b-183">hello output file is as follows:</span></span>

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

<span data-ttu-id="ee53b-184">Este ejemplo muestra un escenario de caso de uso más complicado en la que se utiliza una variable global dentro de una sección de código subyacente que es el conjunto de filas de toohello aplicado toda memoria.</span><span class="sxs-lookup"><span data-stu-id="ee53b-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="ee53b-185">Uso de tipos definidos por el usuario: UDT</span><span class="sxs-lookup"><span data-stu-id="ee53b-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="ee53b-186">Los tipos de definidos por el usuario o UDT constituyen otra característica de programación de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="ee53b-187">UDT de U-SQL actúa como un tipo de definido por el usuario de C# normal.</span><span class="sxs-lookup"><span data-stu-id="ee53b-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="ee53b-188">C# es un lenguaje fuertemente tipado que permite el uso de Hola de tipos integrados y personalizados definidos por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="ee53b-189">U-SQL implícitamente no se puede serializar o deserializar UDT arbitrarios cuando Hola UDT se pasa entre vértices en conjuntos de filas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="ee53b-190">Esto significa que el usuario hello tiene tooprovide un formateador explícita mediante Hola IFormatter interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="ee53b-191">Esto proporciona SQL U con hello serializar y deserializar métodos para hello UDT.</span><span class="sxs-lookup"><span data-stu-id="ee53b-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="ee53b-192">U-SQL extractores integrados y outputters actualmente no se puede serializar o deserializar UDT tooor de datos de archivos, incluso con hello IFormatter conjunto.</span><span class="sxs-lookup"><span data-stu-id="ee53b-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="ee53b-193">Así, cuando escribes tooa archivo de datos UDT con hello instrucción de salida, o que lo lean un extractor de tablas, tendrá que toopass como una cadena o matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="ee53b-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="ee53b-194">A continuación, llama a serialización hello y código (es decir, el método de ToString() Hola UDT) de deserialización explícitamente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="ee53b-195">Extractores de datos definido por el usuario y outputters en hello otra parte, pueden leer y escribir UDT.</span><span class="sxs-lookup"><span data-stu-id="ee53b-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="ee53b-196">Si se intenta toouse UDT en extractor de tablas o OUTPUTTER (fuera de la selección anterior), como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="ee53b-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="ee53b-197">Recibimos Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="ee53b-197">We receive hello following error:</span></span>

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

<span data-ttu-id="ee53b-198">toowork con UDT en outputter, ya sea tenemos tooserialize se toostring con Hola método ToString() o crear un outputter personalizado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="ee53b-199">Actualmente los UDT no se pueden usar en GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="ee53b-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="ee53b-200">Si el UDT se usa GROUP BY, se produce Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="ee53b-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

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

<span data-ttu-id="ee53b-201">toodefine un UDT, tenemos que:</span><span class="sxs-lookup"><span data-stu-id="ee53b-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="ee53b-202">Agregue Hola después de los espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="ee53b-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="ee53b-203">Agregar `Microsoft.Analytics.Interfaces`, lo cual es necesario para las interfaces UDT de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="ee53b-204">Además, `System.IO` podría ser necesario toodefine Hola IFormatter interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="ee53b-205">Defina un tipo definido por el usuario con el atributo SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="ee53b-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="ee53b-206">**SqlUserDefinedType** es toomark usa una definición de tipo en un ensamblado como un tipo definido por el usuario (UDT) en SQL U.</span><span class="sxs-lookup"><span data-stu-id="ee53b-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="ee53b-207">propiedades de Hello del atributo de hello reflejan sus características físicas de Hola de hello UDT.</span><span class="sxs-lookup"><span data-stu-id="ee53b-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="ee53b-208">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-208">This class cannot be inherited.</span></span>

<span data-ttu-id="ee53b-209">SqlUserDefinedType es un atributo necesario para la definición de UDT.</span><span class="sxs-lookup"><span data-stu-id="ee53b-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="ee53b-210">constructor de Hola de clase hello:</span><span class="sxs-lookup"><span data-stu-id="ee53b-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="ee53b-211">SqlUserDefinedTypeAttribute (formateador de tipos)</span><span class="sxs-lookup"><span data-stu-id="ee53b-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="ee53b-212">Formateador de tipo: requiere un formateador UDT--del parámetro toodefine en concreto, el tipo de Hola de hello `IFormatter` interfaz se debe pasar a continuación.</span><span class="sxs-lookup"><span data-stu-id="ee53b-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="ee53b-213">UDT típico también requiere la definición de interfaz de IFormatter hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ee53b-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="ee53b-214">Hola `IFormatter` interfaz serializa y deserializa un gráfico de objetos con el tipo de raíz de Hola de \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="ee53b-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="ee53b-215">\<typeparam nombre = "T" > Hola tipo raíz para tooserialize de gráfico de objeto de Hola y deserializar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="ee53b-216">**Deserializar**: deserializa datos hello en secuencia Hola proporcionado y reconstituye el gráfico de Hola de objetos.</span><span class="sxs-lookup"><span data-stu-id="ee53b-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="ee53b-217">**Serializar**: serializa un objeto o un gráfico de objetos, con hello dada raíz toohello proporciona secuencia.</span><span class="sxs-lookup"><span data-stu-id="ee53b-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="ee53b-218">`MyType`instancia: instancia de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="ee53b-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="ee53b-219">`IColumnWriter`sistema de escritura / `IColumnReader` lector: hello secuencia de la columna subyacente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="ee53b-220">`ISerializationContext`contexto: enumeración que define un conjunto de indicadores que especifica el contexto de origen o destino de Hola para hello secuencia durante la serialización.</span><span class="sxs-lookup"><span data-stu-id="ee53b-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="ee53b-221">**Intermedio**: especifica ese contexto de origen o destino de hello no es un almacén persistente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="ee53b-222">**Persistencia**: especifica ese contexto de origen o destino de hello es un almacén persistente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="ee53b-223">Como un tipo de C# normal, la definición de UDT de U-SQL puede incluir invalidaciones para los operadores como +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="ee53b-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="ee53b-224">Puede incluir también métodos estáticos.</span><span class="sxs-lookup"><span data-stu-id="ee53b-224">It can also include static methods.</span></span> <span data-ttu-id="ee53b-225">Por ejemplo, si vamos toouse este UDT como una función de agregado MIN de U-SQL de parámetro tooa, tenemos toodefine < invalidación de operador.</span><span class="sxs-lookup"><span data-stu-id="ee53b-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="ee53b-226">Anteriormente en esta guía, se muestra un ejemplo de identificación del período fiscal de fecha específicos de hello en formato de hello Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="ee53b-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="ee53b-227">Hola de ejemplo siguiente muestra cómo toodefine personalizado escriba para valores del período fiscales.</span><span class="sxs-lookup"><span data-stu-id="ee53b-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="ee53b-228">A continuación aparece un ejemplo de sección de código subyacente con interfaz IFormatter y UDT personalizados:</span><span class="sxs-lookup"><span data-stu-id="ee53b-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="ee53b-229">tipo definido Hello incluye dos números: trimestre y mes.</span><span class="sxs-lookup"><span data-stu-id="ee53b-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="ee53b-230">Los operadores ==/!=/>/< y el método estático ToString() se definen aquí.</span><span class="sxs-lookup"><span data-stu-id="ee53b-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="ee53b-231">Como se mencionó anteriormente, UDT se puede utilizar en expresiones SELECT, pero no se puede usar en OUTPUTTER/EXTRACTOR sin serialización personalizada.</span><span class="sxs-lookup"><span data-stu-id="ee53b-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="ee53b-232">O bien tiene toobe serializado como una cadena con ToString() o usar con un OUTPUTTER/EXTRACTOR personalizado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="ee53b-233">Ahora vamos a analizar el uso de UDT.</span><span class="sxs-lookup"><span data-stu-id="ee53b-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="ee53b-234">En una sección de código subyacente, hemos cambiado nuestras siguiente de toohello GetFiscalPeriod función:</span><span class="sxs-lookup"><span data-stu-id="ee53b-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

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

<span data-ttu-id="ee53b-235">Como puede ver, devuelve el valor de Hola de nuestro tipo FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="ee53b-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="ee53b-236">En este caso, proporcionamos un ejemplo de cómo toouse más tarde en el script de base de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="ee53b-237">En este ejemplo se muestran distintas maneras de invocación de UDT a partir del script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

<span data-ttu-id="ee53b-238">Este es un ejemplo de una sección de código subyacente completa:</span><span class="sxs-lookup"><span data-stu-id="ee53b-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="ee53b-239">Uso de agregados definidos por el usuario: UDAGG</span><span class="sxs-lookup"><span data-stu-id="ee53b-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="ee53b-240">Los agregados definidos por el usuario son todas las funciones relacionadas con la agregación que no se distribuyen de fábrica con U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="ee53b-241">ejemplo de Hola puede ser un agregado tooperform cálculos matemáticas personalizadas, concatenaciones de cadenas, manipulaciones de cadenas y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="ee53b-242">definición de clase de base agregado definido por el usuario de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="ee53b-242">hello user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="ee53b-243">**SqlUserDefinedAggregate** indica que el tipo de hello debe registrarse como un agregado definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="ee53b-244">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-244">This class cannot be inherited.</span></span>

<span data-ttu-id="ee53b-245">El atributo SqlUserDefinedType es **opcional** para la definición de UDAGG.</span><span class="sxs-lookup"><span data-stu-id="ee53b-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="ee53b-246">Hello clase base permite parámetros abstracta toopass tres: dos como parámetros de entrada y uno de ellos como resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="ee53b-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="ee53b-247">tipos de datos de Hello son variables y deben definirse durante la herencia de clases.</span><span class="sxs-lookup"><span data-stu-id="ee53b-247">hello data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="ee53b-248">**Init** se invoca una vez para cada grupo durante el cálculo.</span><span class="sxs-lookup"><span data-stu-id="ee53b-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="ee53b-249">Proporciona la rutina de inicialización para cada grupo de agregación.</span><span class="sxs-lookup"><span data-stu-id="ee53b-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="ee53b-250">**Accumulate** se ejecuta una vez para cada valor.</span><span class="sxs-lookup"><span data-stu-id="ee53b-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="ee53b-251">Proporciona funcionalidad principal de hello para el algoritmo de agregación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="ee53b-252">Puede ser valores tooaggregate usadas con diversos tipos de datos que se definen durante la herencia de clases.</span><span class="sxs-lookup"><span data-stu-id="ee53b-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="ee53b-253">Puede aceptar dos parámetros de tipos de datos de variable.</span><span class="sxs-lookup"><span data-stu-id="ee53b-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="ee53b-254">**Terminar** se ejecuta una vez por cada grupo de agregación final Hola del resultado de hello toooutput para cada grupo de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="ee53b-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="ee53b-255">entrada correcta toodeclare y tipos de datos de salida, use definición de clase de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="ee53b-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="ee53b-256">T1: Primer parámetro tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="ee53b-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="ee53b-257">T2: Primer parámetro tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="ee53b-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="ee53b-258">TResult: Tipo de valor devuelto de Terminate</span><span class="sxs-lookup"><span data-stu-id="ee53b-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="ee53b-259">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ee53b-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="ee53b-260">o</span><span class="sxs-lookup"><span data-stu-id="ee53b-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="ee53b-261">Uso de UDAGG en U-SQL</span><span class="sxs-lookup"><span data-stu-id="ee53b-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="ee53b-262">toouse UDAGG, primero defina en el código subyacente o referencia a ella desde la programación existente de hello DLL como se indicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ee53b-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="ee53b-263">A continuación, usar hello según la sintaxis:</span><span class="sxs-lookup"><span data-stu-id="ee53b-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="ee53b-264">A continuación se muestra un ejemplo de UDAGG:</span><span class="sxs-lookup"><span data-stu-id="ee53b-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="ee53b-265">Y el script base U-SQL:</span><span class="sxs-lookup"><span data-stu-id="ee53b-265">And base U-SQL script:</span></span>

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

<span data-ttu-id="ee53b-266">En este escenario de caso de uso, se concatena clase GUID para usuarios específicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="ee53b-267">Uso de objetos definidos por el usuario: UDO</span><span class="sxs-lookup"><span data-stu-id="ee53b-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="ee53b-268">U-SQL permite objetos de programación personalizado toodefine, que se denominan objetos definidos por el usuario o UDO.</span><span class="sxs-lookup"><span data-stu-id="ee53b-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="ee53b-269">Hola mostramos una lista de UDO en U-SQL:</span><span class="sxs-lookup"><span data-stu-id="ee53b-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="ee53b-270">Extractores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-270">User-defined extractors</span></span>
    * <span data-ttu-id="ee53b-271">Extraer fila por fila</span><span class="sxs-lookup"><span data-stu-id="ee53b-271">Extract row by row</span></span>
    * <span data-ttu-id="ee53b-272">Utilizar extracción de datos de tooimplement desde archivos estructurados personalizados</span><span class="sxs-lookup"><span data-stu-id="ee53b-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="ee53b-273">Outputters definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-273">User-defined outputters</span></span>
    * <span data-ttu-id="ee53b-274">Dar salida fila por fila</span><span class="sxs-lookup"><span data-stu-id="ee53b-274">Output row by row</span></span>
    * <span data-ttu-id="ee53b-275">Utilizar tipos de datos personalizados de toooutput o formatos de archivo personalizados</span><span class="sxs-lookup"><span data-stu-id="ee53b-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="ee53b-276">Procesadores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-276">User-defined processors</span></span>
    * <span data-ttu-id="ee53b-277">Tomar una fila y producir una fila</span><span class="sxs-lookup"><span data-stu-id="ee53b-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="ee53b-278">Tooreduce usado Hola número de columnas o generar nuevas columnas con valores que se derivan de una columna existente</span><span class="sxs-lookup"><span data-stu-id="ee53b-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="ee53b-279">Aplicadores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-279">User-defined appliers</span></span>
    * <span data-ttu-id="ee53b-280">Tomar una fila y generar 0 filas toon</span><span class="sxs-lookup"><span data-stu-id="ee53b-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="ee53b-281">Se usa con CROSS/OUTER APPLY</span><span class="sxs-lookup"><span data-stu-id="ee53b-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="ee53b-282">Combinadores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-282">User-defined combiners</span></span>
    * <span data-ttu-id="ee53b-283">Combina conjuntos de filas (JOIN definidas por el usuario)</span><span class="sxs-lookup"><span data-stu-id="ee53b-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="ee53b-284">Reductores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-284">User-defined reducers</span></span>
    * <span data-ttu-id="ee53b-285">Tomar n filas y producir una fila</span><span class="sxs-lookup"><span data-stu-id="ee53b-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="ee53b-286">Usar tooreduce Hola un número de filas</span><span class="sxs-lookup"><span data-stu-id="ee53b-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="ee53b-287">UDO se suele llamar explícitamente en el script U-SQL como parte del programa Hola siguiendo las instrucciones SQL U:</span><span class="sxs-lookup"><span data-stu-id="ee53b-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="ee53b-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="ee53b-288">EXTRACT</span></span>
* <span data-ttu-id="ee53b-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="ee53b-289">OUTPUT</span></span>
* <span data-ttu-id="ee53b-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="ee53b-290">PROCESS</span></span>
* <span data-ttu-id="ee53b-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="ee53b-291">COMBINE</span></span>
* <span data-ttu-id="ee53b-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="ee53b-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="ee53b-293">UDO es 0,5 Gb de memoria de tooconsume limitado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="ee53b-294">Esta limitación de memoria no aplica a las ejecuciones de toolocal.</span><span class="sxs-lookup"><span data-stu-id="ee53b-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="ee53b-295">Uso de extractores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-295">Use user-defined extractors</span></span>
<span data-ttu-id="ee53b-296">U-SQL permite tooimport de datos externos mediante una instrucción de extracción.</span><span class="sxs-lookup"><span data-stu-id="ee53b-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="ee53b-297">La instrucción EXTRACT puede utilizar extractores UDO integrados:</span><span class="sxs-lookup"><span data-stu-id="ee53b-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="ee53b-298">*Extractors.Text()*: Proporciona extracción de archivos de texto delimitado de diferentes codificaciones.</span><span class="sxs-lookup"><span data-stu-id="ee53b-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="ee53b-299">*Extractors.Csv()*: Proporciona extracción de archivos de valores separados por comas (CSV) de diferentes codificaciones.</span><span class="sxs-lookup"><span data-stu-id="ee53b-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="ee53b-300">*Extractors.Tsv()*: Proporciona extracción de archivos de valores separados por tabulaciones (TSV) de diferentes codificaciones.</span><span class="sxs-lookup"><span data-stu-id="ee53b-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="ee53b-301">Puede ser útil toodevelop un extractor de datos personalizado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="ee53b-302">Esto puede resultar útil durante la importación de datos si queremos toodo cualquiera de hello siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="ee53b-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="ee53b-303">Modificar datos de entrada mediante la división de columnas y modificar valores individuales.</span><span class="sxs-lookup"><span data-stu-id="ee53b-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="ee53b-304">Hola funcionalidad del procesador es mejor para combinar las columnas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="ee53b-305">Analizar datos no estructurados, como páginas web o correos electrónicos o datos parcialmente no estructurados, como XML o JSON.</span><span class="sxs-lookup"><span data-stu-id="ee53b-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="ee53b-306">Analizar datos en codificación no compatible.</span><span class="sxs-lookup"><span data-stu-id="ee53b-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="ee53b-307">toodefine extractor de tablas definidas por el usuario, o uir, tenemos toocreate un `IExtractor` interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="ee53b-308">Todos los extractor de tablas de parámetros toohello, de entrada, como delimitadores de columna o fila y la codificación, deben toobe definido en hello constructor de clase hello.</span><span class="sxs-lookup"><span data-stu-id="ee53b-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="ee53b-309">Hola `IExtractor` interfaz también debe contener una definición de hello `IEnumerable<IRow>` invalidar como sigue:</span><span class="sxs-lookup"><span data-stu-id="ee53b-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="ee53b-310">Hola **SqlUserDefinedExtractor** atributo indica que el tipo de hello debe registrarse como un extractor de tablas definidas por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="ee53b-311">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-311">This class cannot be inherited.</span></span>

<span data-ttu-id="ee53b-312">SqlUserDefinedExtractor es un atributo opcional para la definición de UDE.</span><span class="sxs-lookup"><span data-stu-id="ee53b-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="ee53b-313">Utiliza toodefine AtomicFileProcessing propiedad para el objeto de uir Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="ee53b-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="ee53b-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="ee53b-315">**true** = Indica que este extractor requiere archivos de entrada atómicos (JSON, XML...)</span><span class="sxs-lookup"><span data-stu-id="ee53b-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="ee53b-316">**false** = Indica que este extractor puede tratar con archivos divididos o distribuidos (CSV, SEQ...)</span><span class="sxs-lookup"><span data-stu-id="ee53b-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="ee53b-317">objetos de programación de Hello principales uir son **entrada** y **salida**.</span><span class="sxs-lookup"><span data-stu-id="ee53b-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="ee53b-318">objeto de entrada de Hello es tooenumerate usa datos de entrada como `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="ee53b-319">objeto de salida de Hello es tooset usa datos de salida como resultado de la actividad de hello extractor de tablas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="ee53b-320">se tiene acceso a datos de entrada de Hola a través de `System.IO.Stream` y `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="ee53b-321">Para la enumeración de las columnas de entrada, en primer lugar dividiremos flujo de entrada de hello utilizando un delimitador de filas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="ee53b-322">Después, dividiremos aún más la fila de entrada en partes de la columna.</span><span class="sxs-lookup"><span data-stu-id="ee53b-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="ee53b-323">tooset los datos de salida, usaremos hello `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="ee53b-324">Es importante toounderstand que Hola extractor personalizado genera solo las columnas y los valores que se definen con salida de hello.</span><span class="sxs-lookup"><span data-stu-id="ee53b-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="ee53b-325">Establezca la llamada del método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="ee53b-326">salida de Hello extractor reales se desencadena mediante una llamada a `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ee53b-327">Aquí te mostramos hello (ejemplo) extractor de tablas:</span><span class="sxs-lookup"><span data-stu-id="ee53b-327">Following is hello extractor example:</span></span>

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

<span data-ttu-id="ee53b-328">En este escenario de caso de uso, extractor de Hola Hola GUID para la columna "guid", vuelve a generar y convierte los valores de hello de caso de tooupper de columna de "usuario".</span><span class="sxs-lookup"><span data-stu-id="ee53b-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="ee53b-329">Los extractores personalizados pueden producir resultados más complicados mediante el análisis de datos de entrada y la manipulación de estos.</span><span class="sxs-lookup"><span data-stu-id="ee53b-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="ee53b-330">Este es un script base U-SQL que utiliza un extractor personalizado:</span><span class="sxs-lookup"><span data-stu-id="ee53b-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

## <a name="use-user-defined-outputters"></a><span data-ttu-id="ee53b-331">Uso de outputters definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-331">Use user-defined outputters</span></span>
<span data-ttu-id="ee53b-332">Outputter definido por el usuario es UDO SQL U otro que permite la funcionalidad integrada de U-SQL de tooextend.</span><span class="sxs-lookup"><span data-stu-id="ee53b-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="ee53b-333">Extractor de tablas toohello similar, hay varios outputters integrados.</span><span class="sxs-lookup"><span data-stu-id="ee53b-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="ee53b-334">*Outputters.Text()*: escribe datos toodelimited archivos de texto de diferentes codificaciones.</span><span class="sxs-lookup"><span data-stu-id="ee53b-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="ee53b-335">*Outputters.Csv()*: escribe datos toocomma de valores separados archivos (CSV) de diferentes codificaciones.</span><span class="sxs-lookup"><span data-stu-id="ee53b-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="ee53b-336">*Outputters.Tsv()*: escribe datos tootab de valores separados archivos (TSV) de diferentes codificaciones.</span><span class="sxs-lookup"><span data-stu-id="ee53b-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="ee53b-337">Outputter personalizado permite toowrite datos en un formato personalizado definido.</span><span class="sxs-lookup"><span data-stu-id="ee53b-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="ee53b-338">Esto puede ser útil para hello siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="ee53b-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="ee53b-339">Escribir archivos de datos de toosemi estructurados o no estructurados.</span><span class="sxs-lookup"><span data-stu-id="ee53b-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="ee53b-340">Escribir datos en codificaciones no admitidas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="ee53b-341">Modificar datos de salida o agregar atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="ee53b-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="ee53b-342">toodefine definido por el usuario outputter, necesitamos hello toocreate `IOutputter` interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="ee53b-343">Aquí te mostramos Hola base `IOutputter` la implementación de clase:</span><span class="sxs-lookup"><span data-stu-id="ee53b-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="ee53b-344">Todos los parámetros toohello outputter, de entrada, como delimitadores de columna o fila, la codificación y así sucesivamente, deben toobe definido en hello constructor de clase hello.</span><span class="sxs-lookup"><span data-stu-id="ee53b-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="ee53b-345">Hola `IOutputter` interfaz también debe contener una definición para `void Output` invalidar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="ee53b-346">atributo de Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` , opcionalmente, se puede establecer para el procesamiento de archivos atómica.</span><span class="sxs-lookup"><span data-stu-id="ee53b-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="ee53b-347">Para obtener más información, vea Hola detalles siguientes.</span><span class="sxs-lookup"><span data-stu-id="ee53b-347">For more information, see hello following details.</span></span>

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

* <span data-ttu-id="ee53b-348">`Output` se llama para cada fila de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee53b-348">`Output` is called for each input row.</span></span> <span data-ttu-id="ee53b-349">Devuelve hello `IUnstructuredWriter output` conjunto de filas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="ee53b-350">se utiliza Hola clase del Constructor definido por el usuario outputter de toopass parámetros toohello.</span><span class="sxs-lookup"><span data-stu-id="ee53b-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="ee53b-351">`Close`se utiliza toooptionally invalidar toorelease costoso estado o para determinar cuándo se escribió la última fila de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="ee53b-352">**SqlUserDefinedOutputter** atributo indica que el tipo de hello debe registrarse como un outputter definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="ee53b-353">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-353">This class cannot be inherited.</span></span>

<span data-ttu-id="ee53b-354">SqlUserDefinedOutputter es un atributo opcional para la definición del outputter definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="ee53b-355">Ha utilizado la propiedad AtomicFileProcessing de toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="ee53b-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="ee53b-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="ee53b-357">**true** = Indica que este outputter requiere archivos de salida atómicos (JSON, XML...)</span><span class="sxs-lookup"><span data-stu-id="ee53b-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="ee53b-358">**false** = Indica que este outputter puede tratar con archivos divididos o distribuidos (CSV, SEQ...)</span><span class="sxs-lookup"><span data-stu-id="ee53b-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="ee53b-359">los objetos de programación principal Hola son **fila** y **salida**.</span><span class="sxs-lookup"><span data-stu-id="ee53b-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="ee53b-360">Hola **fila** objeto es tooenumerate usa datos de salida como `IRow` interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="ee53b-361">**Salida** es archivo de destino de toohello de datos de salida de tooset usado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="ee53b-362">Hello datos de salida se tiene acceso a través de hello `IRow` interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="ee53b-363">Los datos de salida pasan una fila en cada momento.</span><span class="sxs-lookup"><span data-stu-id="ee53b-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="ee53b-364">se enumeran los valores individuales de Hello llamando al método Get hello de interfaz IRow de hello:</span><span class="sxs-lookup"><span data-stu-id="ee53b-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="ee53b-365">Los nombres de columna individuales se pueden determinar mediante una llamada a `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="ee53b-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="ee53b-366">Este enfoque permite toobuild un outputter flexible para cualquier esquema de metadatos.</span><span class="sxs-lookup"><span data-stu-id="ee53b-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="ee53b-367">Hello datos de salida se escriben toofile utilizando `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="ee53b-368">parámetro de la secuencia de Hola se establece demasiado`output.BaseStrea` como parte de `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="ee53b-369">Tenga en cuenta que es importante tooflush Hola datos búfer toohello archivo después de cada iteración de la fila.</span><span class="sxs-lookup"><span data-stu-id="ee53b-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="ee53b-370">Además, Hola `StreamWriter` objeto debe utilizarse con hello descartables atributo habilitado (valor predeterminado) y con hello **con** palabra clave:</span><span class="sxs-lookup"><span data-stu-id="ee53b-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="ee53b-371">De lo contrario, llame al método Flush() explícitamente después de cada iteración.</span><span class="sxs-lookup"><span data-stu-id="ee53b-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="ee53b-372">Esto se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="ee53b-373">Establecimiento de encabezados y pies de página para el outputter definido por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="ee53b-374">tooset un encabezado, use el flujo de ejecución de la iteración.</span><span class="sxs-lookup"><span data-stu-id="ee53b-374">tooset a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="ee53b-375">Hola código de hello primero `if (isHeaderRow)` bloque se ejecuta solo una vez.</span><span class="sxs-lookup"><span data-stu-id="ee53b-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="ee53b-376">Pie de página de hello, usar la instancia de toohello de referencia de Hola de `System.IO.Stream` objeto (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="ee53b-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="ee53b-377">Escribir el pie de página de Hola Hola método Close() de hello `IOutputter` interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="ee53b-378">(Para obtener más información, vea la siguiente ejemplo de Hola.)</span><span class="sxs-lookup"><span data-stu-id="ee53b-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="ee53b-379">Este es un ejemplo de un outputter definido por el usuario:</span><span class="sxs-lookup"><span data-stu-id="ee53b-379">Following is an example of a user-defined outputter:</span></span>

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

<span data-ttu-id="ee53b-380">Y el script base U-SQL:</span><span class="sxs-lookup"><span data-stu-id="ee53b-380">And U-SQL base script:</span></span>

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

<span data-ttu-id="ee53b-381">Se trata de un outputter HTML que crea un archivo HTML con los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="ee53b-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="ee53b-382">Llamada a un outputter desde el script base U-SQL</span><span class="sxs-lookup"><span data-stu-id="ee53b-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="ee53b-383">toocall un outputter personalizado desde un script de SQL U base hello, Hola nueva instancia del objeto de hello outputter tiene toobe creado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="ee53b-384">tooavoid crear una instancia del programa Hola a objeto en un script de base, podemos crear un contenedor de la función, como se muestra en el ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="ee53b-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

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

<span data-ttu-id="ee53b-385">En este caso, llamada original Hola Hola siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="ee53b-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="ee53b-386">Uso de procesadores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-386">Use user-defined processors</span></span>
<span data-ttu-id="ee53b-387">Procesador definido por el usuario o UDP, es un tipo de UDO U-SQL que permite las filas entrantes tooprocess Hola aplicando características de programación.</span><span class="sxs-lookup"><span data-stu-id="ee53b-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="ee53b-388">UDP permite toocombine columnas, modifique los valores y agregar nuevas columnas si es necesario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="ee53b-389">Básicamente, ayuda a tooprocess unos elementos de datos de conjunto de filas tooproduce necesario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="ee53b-390">toodefine un UDP, necesitamos toocreate una `IProcessor` interfaz con hello `SqlUserDefinedProcessor` atributo, que es opcional para UDP.</span><span class="sxs-lookup"><span data-stu-id="ee53b-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="ee53b-391">Esta interfaz debe contener la definición de Hola para hello `IRow` invalidar el conjunto de filas de interfaz, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ee53b-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

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

<span data-ttu-id="ee53b-392">**SqlUserDefinedProcessor** indica que el tipo de hello debe registrarse como un procesador definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="ee53b-393">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-393">This class cannot be inherited.</span></span>

<span data-ttu-id="ee53b-394">atributo de Hello SqlUserDefinedProcessor es **opcional** para la definición de UDP.</span><span class="sxs-lookup"><span data-stu-id="ee53b-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="ee53b-395">los objetos de programación principal Hola son **entrada** y **salida**.</span><span class="sxs-lookup"><span data-stu-id="ee53b-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="ee53b-396">objeto de entrada de Hello es tooenumerate usa las columnas de entrada y salida y datos de salida de tooset como resultado de la actividad del procesador Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="ee53b-397">Para la enumeración de las columnas de entrada, usamos hello `input.Get` método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="ee53b-398">Hola parámetro `input.Get` método es una columna que se pasa como parte del programa Hola a `PRODUCE` cláusula de hello `PROCESS` instrucción de script de base de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="ee53b-399">Necesitamos toouse datos correctos de hello escriba aquí.</span><span class="sxs-lookup"><span data-stu-id="ee53b-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="ee53b-400">Para la salida, usar hello `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="ee53b-401">Es importante toonote ese productor personalizado solo genera columnas y valores que se definen con hello `output.Set` llamada al método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="ee53b-402">salida de Hello real del procesador se activa mediante una llamada a `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ee53b-403">Este es un ejemplo de procesador:</span><span class="sxs-lookup"><span data-stu-id="ee53b-403">Following is a processor example:</span></span>

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

<span data-ttu-id="ee53b-404">En este escenario de caso de uso, el procesador de hello está generando una nueva columna denominada "full_description" mediante la combinación de hello las columnas existentes: en este caso, "usuario" en mayúsculas y "des".</span><span class="sxs-lookup"><span data-stu-id="ee53b-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="ee53b-405">También se vuelve a generar un GUID y se devuelve Hola originales y los nuevos valores GUID.</span><span class="sxs-lookup"><span data-stu-id="ee53b-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="ee53b-406">Como puede ver de ejemplo de Hola a anterior, puede llamar a métodos de C# durante `output.Set` llamada al método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="ee53b-407">Este es un ejemplo de script U-SQL base que utiliza un procesador personalizado:</span><span class="sxs-lookup"><span data-stu-id="ee53b-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

## <a name="use-user-defined-appliers"></a><span data-ttu-id="ee53b-408">Uso de aplicadores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-408">Use user-defined appliers</span></span>
<span data-ttu-id="ee53b-409">Un aplicador de U-SQL definido por el usuario permite función tooinvoke personalizado C# para cada fila devuelta por la expresión de tabla externa de Hola de una consulta.</span><span class="sxs-lookup"><span data-stu-id="ee53b-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="ee53b-410">Hola de entrada derecha se evalúa para cada fila de entrada izquierda hello y filas de hello producidas se combinan para la salida final Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="ee53b-411">Hola lista de columnas que se producen por el operador APPLY de Hola son la combinación de Hola de conjunto de Hola de columnas de la izquierda de Hola y Hola de entrada derecha.</span><span class="sxs-lookup"><span data-stu-id="ee53b-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="ee53b-412">Se está llamando a aplicador definido por el usuario como parte del programa Hola USQL seleccione expresión.</span><span class="sxs-lookup"><span data-stu-id="ee53b-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="ee53b-413">Hola llamada típica toohello definido por el usuario aplicador parece Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee53b-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="ee53b-414">Consulte [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (U-SQL SELECT, selección de CROSS APPLY y OUTER APPLY) para más información sobre cómo utilizar aplicadores en una expresión SELECT.</span><span class="sxs-lookup"><span data-stu-id="ee53b-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="ee53b-415">definición de clase base aplicador de Hello definido por el usuario es como sigue:</span><span class="sxs-lookup"><span data-stu-id="ee53b-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="ee53b-416">toodefine un aplicador definido por el usuario, necesitamos hello toocreate `IApplier` interfaz con hello [`SqlUserDefinedApplier`] atributo, que es opcional para una definición de aplicador definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="ee53b-417">Aplicar se llama para cada fila de tabla externa Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="ee53b-418">Devuelve hello `IUpdatableRow` conjunto de filas de salida.</span><span class="sxs-lookup"><span data-stu-id="ee53b-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="ee53b-419">clase de Constructor Hello es toopass usa parámetros toohello definido por el usuario aplicador.</span><span class="sxs-lookup"><span data-stu-id="ee53b-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="ee53b-420">**SqlUserDefinedApplier** indica que el tipo de hello debe registrarse como un aplicador definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="ee53b-421">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-421">This class cannot be inherited.</span></span>

<span data-ttu-id="ee53b-422">**SqlUserDefinedApplier** es **opcional** para la definición del aplicador definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="ee53b-423">objetos de programación principales de Hello son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ee53b-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="ee53b-424">Los conjuntos de filas de entrada se pasan como entrada `IRow`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="ee53b-425">Hello salida se generan filas como `IUpdatableRow` interfaz de salida.</span><span class="sxs-lookup"><span data-stu-id="ee53b-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="ee53b-426">Nombres de columna individuales se pueden determinar mediante llamada hello `IRow` método de esquema.</span><span class="sxs-lookup"><span data-stu-id="ee53b-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="ee53b-427">valores de datos reales de hello tooget de Hola entrante `IRow`, usamos hello Get() método `IRow` interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="ee53b-428">O bien, se utiliza el nombre de columna del esquema de hello:</span><span class="sxs-lookup"><span data-stu-id="ee53b-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="ee53b-429">Hello valores de salida deben establecerse con `IUpdatableRow` salida:</span><span class="sxs-lookup"><span data-stu-id="ee53b-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="ee53b-430">Es importante toounderstand que aplicadores personalizados sólo genera resultados columnas y valores que se definen con `output.Set` llamada al método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="ee53b-431">salida real de Hola se desencadena mediante una llamada a `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ee53b-432">se pueden pasar parámetros aplicador de Hello definidos por el usuario toohello constructor.</span><span class="sxs-lookup"><span data-stu-id="ee53b-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="ee53b-433">Aplicador de puede devolver un número variable de columnas que deben toobe definido durante la llamada aplicador de hello en el Script U-SQL base.</span><span class="sxs-lookup"><span data-stu-id="ee53b-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="ee53b-434">Este es ejemplo aplicador de hello definido por el usuario:</span><span class="sxs-lookup"><span data-stu-id="ee53b-434">Here is hello user-defined applier example:</span></span>

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

<span data-ttu-id="ee53b-435">Aquí te mostramos Hola base U-secuencia de comandos SQL para este aplicador definido por el usuario:</span><span class="sxs-lookup"><span data-stu-id="ee53b-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

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

<span data-ttu-id="ee53b-436">En este escenario de caso de uso, definido por el usuario aplicador actúa como un analizador de valores delimitados por comas para automóvil Hola flota propiedades.</span><span class="sxs-lookup"><span data-stu-id="ee53b-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="ee53b-437">filas del archivo de entrada de Hello aspecto Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee53b-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="ee53b-438">Es un archivo TSV delimitado por tabulaciones típico con la columna de propiedades que contiene las propiedades de los automóviles, como la marca y el modelo.</span><span class="sxs-lookup"><span data-stu-id="ee53b-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="ee53b-439">Esas propiedades deben ser columnas de la tabla de toohello analizado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="ee53b-440">aplicador de Hola que se proporciona también le permite toogenerate conjunto de filas, en función de hello parámetro que se pasa como resultado un número de propiedades en hello dinámico.</span><span class="sxs-lookup"><span data-stu-id="ee53b-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="ee53b-441">Puede generar todas las propiedades o solo un conjunto específico de propiedades.</span><span class="sxs-lookup"><span data-stu-id="ee53b-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="ee53b-442">aplicador de Hello definido por el usuario se pueda llamar como una nueva instancia de objeto aplicador:</span><span class="sxs-lookup"><span data-stu-id="ee53b-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="ee53b-443">O con la invocación de Hola de un método de fábrica de contenedor:</span><span class="sxs-lookup"><span data-stu-id="ee53b-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="ee53b-444">Uso de combinadores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-444">Use user-defined combiners</span></span>
<span data-ttu-id="ee53b-445">Combinador definido por el usuario, o UDC, le permite toocombine filas de conjuntos de filas izquierdo y derecho, en función de la lógica personalizada.</span><span class="sxs-lookup"><span data-stu-id="ee53b-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="ee53b-446">El combinador definido por el usuario se utiliza con la expresión de COMBINE.</span><span class="sxs-lookup"><span data-stu-id="ee53b-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="ee53b-447">Se está llamando a un Combinador con expresión de combinación de Hola que proporciona Hola información necesaria sobre ambos conjuntos de filas de entrada de hello, Hola agrupación de columnas, hello espera esquema resultados e información adicional.</span><span class="sxs-lookup"><span data-stu-id="ee53b-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="ee53b-448">toocall un Combinador en un script U-SQL base, utilizamos Hola según la sintaxis:</span><span class="sxs-lookup"><span data-stu-id="ee53b-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

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

<span data-ttu-id="ee53b-449">Para más información, vea [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx) (Expresión COMBINE (U-SQL)).</span><span class="sxs-lookup"><span data-stu-id="ee53b-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="ee53b-450">toodefine un Combinador definido por el usuario, necesitamos hello toocreate `ICombiner` interfaz con hello [`SqlUserDefinedCombiner`] atributo, que es opcional para una definición de Combinador definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="ee53b-451">Definición de clase base `ICombiner`:</span><span class="sxs-lookup"><span data-stu-id="ee53b-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="ee53b-452">Hola implementación personalizada de un `ICombiner` interfaz debe contener la definición de Hola para un `IEnumerable<IRow>` combinar invalidación.</span><span class="sxs-lookup"><span data-stu-id="ee53b-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="ee53b-453">Hola **SqlUserDefinedCombiner** atributo indica que el tipo de hello debe registrarse como un Combinador definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="ee53b-454">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-454">This class cannot be inherited.</span></span>

<span data-ttu-id="ee53b-455">**SqlUserDefinedCombiner** es propiedad de modo de Combinador de hello toodefine usado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="ee53b-456">Es un atributo opcional para la definición de un combinador definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="ee53b-457">Modo CombinerMode</span><span class="sxs-lookup"><span data-stu-id="ee53b-457">CombinerMode     Mode</span></span>

<span data-ttu-id="ee53b-458">Enumeración CombinerMode puede tomar Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="ee53b-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="ee53b-459">Completo (0), de que cada fila de resultados depende potencialmente de todas las filas de entrada de Hola izquierda y derecha con hello mismo valor de clave.</span><span class="sxs-lookup"><span data-stu-id="ee53b-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="ee53b-460">Izquierda (1), cada fila de salida depende de una sola fila de entrada de hello izquierda (y potencialmente todas las filas de hello derecha con hello mismo valor de clave).</span><span class="sxs-lookup"><span data-stu-id="ee53b-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="ee53b-461">Derecha (2), cada fila de salida depende de una sola fila de entrada de hello derecho (y potencialmente todas las filas de hello izquierda con hello mismo valor de clave).</span><span class="sxs-lookup"><span data-stu-id="ee53b-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="ee53b-462">Interna (3), cada fila de salida depende de una sola entrada de fila de la izquierda y derecha con hello igual valor.</span><span class="sxs-lookup"><span data-stu-id="ee53b-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="ee53b-463">Ejemplo:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="ee53b-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="ee53b-464">objetos de programación principal Hola son:</span><span class="sxs-lookup"><span data-stu-id="ee53b-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="ee53b-465">Los conjuntos de filas de entrada se pasan como el tipo de interfaz `IRowset` **left** y **right**.</span><span class="sxs-lookup"><span data-stu-id="ee53b-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="ee53b-466">Ambos conjuntos de filas deben enumerarse para su procesamiento.</span><span class="sxs-lookup"><span data-stu-id="ee53b-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="ee53b-467">Sólo puede enumerar cada interfaz una vez, por lo que tiene tooenumerate y almacenarla en la caché si es necesario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="ee53b-468">Para el almacenamiento en caché, se puede crear un tipo de estructura de memoria List\<T\> como resultado de la ejecución de la consulta LINQ y, más concretamente, List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="ee53b-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="ee53b-469">tipo de datos anónimos Hola puede usarse durante la enumeración también.</span><span class="sxs-lookup"><span data-stu-id="ee53b-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="ee53b-470">Vea [Introducción tooLINQ consultas (C#)](https://msdn.microsoft.com/library/bb397906.aspx) para obtener más información acerca de las consultas LINQ, y [IEnumerable\<T\> interfaz](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) para obtener más información acerca de IEnumerable\<T\> interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="ee53b-471">valores de datos reales de hello tooget de Hola entrante `IRowset`, usamos hello Get() método `IRow` interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="ee53b-472">Nombres de columna individuales se pueden determinar mediante llamada hello `IRow` método de esquema.</span><span class="sxs-lookup"><span data-stu-id="ee53b-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="ee53b-473">O mediante el nombre de columna del esquema de hello:</span><span class="sxs-lookup"><span data-stu-id="ee53b-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="ee53b-474">enumeración general de Hello con LINQ es similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee53b-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="ee53b-475">Después de enumerar los conjuntos de filas, vamos tooloop a través de todas las filas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="ee53b-476">Para cada fila de conjunto de filas izquierdo hello, vamos toofind todas las filas que cumplen la condición de Hola de nuestro Combinador.</span><span class="sxs-lookup"><span data-stu-id="ee53b-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="ee53b-477">Hello valores de salida deben establecerse con `IUpdatableRow` salida.</span><span class="sxs-lookup"><span data-stu-id="ee53b-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="ee53b-478">salida real de Hola se desencadena mediante una llamada a demasiado`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ee53b-479">Este es un ejemplo de combinador:</span><span class="sxs-lookup"><span data-stu-id="ee53b-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="ee53b-480">En este escenario de caso de uso, estamos creando un informe de análisis para el distribuidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="ee53b-481">objetivo de Hello es toofind todos los productos cuyo costo es más de 20.000 USD y que se venden a través del sitio Web de hello más rápido que a través de distribuidor regular de hello dentro de un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="ee53b-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="ee53b-482">Este es el script U-SQL base de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee53b-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="ee53b-483">Puede comparar la lógica de hello entre una combinación normal y un Combinador:</span><span class="sxs-lookup"><span data-stu-id="ee53b-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

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

<span data-ttu-id="ee53b-484">Un Combinador definido por el usuario se pueda llamar como una nueva instancia de objeto aplicador de hello:</span><span class="sxs-lookup"><span data-stu-id="ee53b-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="ee53b-485">O con la invocación de Hola de un método de fábrica de contenedor:</span><span class="sxs-lookup"><span data-stu-id="ee53b-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="ee53b-486">Uso de reductores definidos por el usuario</span><span class="sxs-lookup"><span data-stu-id="ee53b-486">Use user-defined reducers</span></span>

<span data-ttu-id="ee53b-487">U-SQL permite toowrite reductores de conjunto de filas personalizadas en C# con marco de extensibilidad de hello operador definido por el usuario e implementando una interfaz IReducer.</span><span class="sxs-lookup"><span data-stu-id="ee53b-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="ee53b-488">Reductor definido por el usuario, o UDR, puede ser las filas innecesarias tooeliminate usado durante la extracción de datos (importar).</span><span class="sxs-lookup"><span data-stu-id="ee53b-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="ee53b-489">También puede ser usado toomanipulate y evaluar las filas y columnas.</span><span class="sxs-lookup"><span data-stu-id="ee53b-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="ee53b-490">En función de la lógica de programación, también puede definir qué filas necesitan toobe extraído.</span><span class="sxs-lookup"><span data-stu-id="ee53b-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="ee53b-491">una clase UDR toodefine, necesitamos toocreate una `IReducer` interfaz con una función opcional `SqlUserDefinedReducer` atributo.</span><span class="sxs-lookup"><span data-stu-id="ee53b-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="ee53b-492">Esta interfaz de clase debe contener una definición de hello `IEnumerable` invalidar el conjunto de filas de interfaz.</span><span class="sxs-lookup"><span data-stu-id="ee53b-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="ee53b-493">Hola **SqlUserDefinedReducer** atributo indica que el tipo de hello debe registrarse como un reductor definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="ee53b-494">Esta clase no se puede heredar.</span><span class="sxs-lookup"><span data-stu-id="ee53b-494">This class cannot be inherited.</span></span>
<span data-ttu-id="ee53b-495">**SqlUserDefinedReducer** es un atributo opcional para la definición del reductor definido por el usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="ee53b-496">Ha utilizado toodefine IsRecursive propiedad.</span><span class="sxs-lookup"><span data-stu-id="ee53b-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="ee53b-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="ee53b-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="ee53b-498">**true**  = Indica si el reductor es idempotente</span><span class="sxs-lookup"><span data-stu-id="ee53b-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="ee53b-499">los objetos de programación principal Hola son **entrada** y **salida**.</span><span class="sxs-lookup"><span data-stu-id="ee53b-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="ee53b-500">objeto de entrada de Hello es tooenumerate usado filas de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee53b-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="ee53b-501">Salida es tooset usado filas de salida como resultado de la reducción de actividad.</span><span class="sxs-lookup"><span data-stu-id="ee53b-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="ee53b-502">Para la enumeración de filas de entrada, usamos hello `Row.Get` método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="ee53b-503">Hola parámetro hello `Row.Get` método es una columna que se pasa como parte del programa Hola a `PRODUCE` clase de hello `REDUCE` instrucción de script de base de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee53b-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="ee53b-504">Necesitamos toouse Hola tipo de datos correcto aquí también.</span><span class="sxs-lookup"><span data-stu-id="ee53b-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="ee53b-505">Para la salida, usar hello `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="ee53b-506">Es importante toounderstand que valores salidas solo reductor personalizados que se definen con Hola `output.Set` llamada al método.</span><span class="sxs-lookup"><span data-stu-id="ee53b-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="ee53b-507">salida de Hello reductor reales se desencadena mediante una llamada a `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="ee53b-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="ee53b-508">Este es un ejemplo de reductor:</span><span class="sxs-lookup"><span data-stu-id="ee53b-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="ee53b-509">En este escenario de caso de uso, omite el reductor Hola filas con un nombre de usuario vacío.</span><span class="sxs-lookup"><span data-stu-id="ee53b-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="ee53b-510">Para cada fila de conjunto de filas, lee cada columna necesaria y después se evalúa como longitud de Hola Hola del nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="ee53b-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="ee53b-511">Produce el resultado real de la fila Hola solo si la longitud del valor de nombre de usuario es mayor que 0.</span><span class="sxs-lookup"><span data-stu-id="ee53b-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="ee53b-512">Este es un script base U-SQL que utiliza un reductor personalizado:</span><span class="sxs-lookup"><span data-stu-id="ee53b-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
