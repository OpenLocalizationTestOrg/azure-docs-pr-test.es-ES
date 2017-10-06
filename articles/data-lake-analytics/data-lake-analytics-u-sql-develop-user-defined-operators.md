---
title: aaaDevelop U-SQL los operadores definidos por el usuario (UDO) | Documentos de Microsoft
description: "Obtenga información acerca de cómo se usa y reutiliza en los análisis de Data Lake trabajos toodevelop operadores definidos por el usuario toobe. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a>Desarrollo de operadores U-SQL definidos por el usuario (UDO)
Obtenga información acerca de cómo toodevelop definido por el usuario datos tooprocess de operadores en un trabajo de SQL U.

Para instrucciones sobre cómo desarrollar ensamblados de propósito general para U-SQL, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a>Definición y uso de un operador definido por el usuario en U-SQL
**toocreate y enviar un trabajo de SQL U**

1. En Visual Studio Hola seleccione **archivo > Nuevo > proyecto > U-SQL proyecto**.
2. Haga clic en **Aceptar**. Visual Studio crea una solución con un archivo Script.usql.
3. En el **Explorador de soluciones**, expanda Script.usql y haga doble clic en **Script.usql.cs**.
4. Pegue Hola siguiente código en el archivo hello:

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. Abra **Script.usql**, y pegar Hola siguiendo script U-SQL:

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. Especifique la cuenta de análisis de Data Lake hello, base de datos y esquema.
8. En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Build Script** (Compilar script).
9. En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Submit Script** (Enviar script).
10. Si aún no lo ha conectado tooyour suscripción de Azure, que se van a ser solicitada tooenter sus credenciales de cuenta de Azure.
11. Haga clic en **Enviar**. Resultados de envío y de vínculo de trabajo están disponibles en la ventana de resultados de hello cuando se completa el envío de Hola.
12. Haga clic en hello **actualizar** botón toosee hello más reciente trabajo estado y la actualización de pantalla de bienvenida.

**salida de hello toosee**

1. De **Explorador de servidores**, expanda **Azure**, expanda **análisis de Data Lake**, expanda y su cuenta de análisis de Data Lake **decuentasdealmacenamiento**, haga clic en hello almacenamiento predeterminado y, a continuación, haga clic en **Explorer**.
2. Expanda Ejemplos, expanda Salidas y, finalmente, haga doble clic en **Drivers.csv**.

## <a name="see-also"></a>Otras referencias
* [Introducción a Análisis de Data Lake mediante PowerShell](data-lake-analytics-get-started-powershell.md)
* [Empezar a trabajar con análisis de Data Lake con hello portal de Azure](data-lake-analytics-get-started-portal.md)
* [Uso de Data Lake Tools for Visual Studio para desarrollar aplicaciones de U-SQL](data-lake-analytics-data-lake-tools-get-started.md)
