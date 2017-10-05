---
title: Desarrollo de operadores U-SQL definidos por el usuario (UDO) | Microsoft Docs
description: "Aprenda a desarrollar operadores definidos por el usuario para usarse y volverse a usar en trabajos de Análisis de Data Lake. "
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
ms.openlocfilehash: fdee02fb60b633c26704fc1774dfc3a7825b5e0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="0a433-103">Desarrollo de operadores U-SQL definidos por el usuario (UDO)</span><span class="sxs-lookup"><span data-stu-id="0a433-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="0a433-104">Aprenda a desarrollar operadores definidos por el usuario para procesar datos en un trabajo de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0a433-104">Learn how to develop user-defined operators to process data in a U-SQL job.</span></span>

<span data-ttu-id="0a433-105">Para instrucciones sobre cómo desarrollar ensamblados de propósito general para U-SQL, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="0a433-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="0a433-106">Definición y uso de un operador definido por el usuario en U-SQL</span><span class="sxs-lookup"><span data-stu-id="0a433-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="0a433-107">**Para crear y enviar un trabajo de U-SQL**</span><span class="sxs-lookup"><span data-stu-id="0a433-107">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="0a433-108">En el menú de Visual Studio, seleccione **Archivo > Nuevo > Proyecto > U-SQL Project** (Proyecto de U-SQL).</span><span class="sxs-lookup"><span data-stu-id="0a433-108">From the Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="0a433-109">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0a433-109">Click **OK**.</span></span> <span data-ttu-id="0a433-110">Visual Studio crea una solución con un archivo Script.usql.</span><span class="sxs-lookup"><span data-stu-id="0a433-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="0a433-111">En el **Explorador de soluciones**, expanda Script.usql y haga doble clic en **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="0a433-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="0a433-112">Pegue el código siguiente en el archivo:</span><span class="sxs-lookup"><span data-stu-id="0a433-112">Paste the following code into the file:</span></span>

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
6. <span data-ttu-id="0a433-113">Abra **Script.usql** y pegue el siguiente script de U-SQL:</span><span class="sxs-lookup"><span data-stu-id="0a433-113">Open **Script.usql**, and paste the following U-SQL script:</span></span>

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
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="0a433-114">Especifique la cuenta de Análisis de Data Lake, la base de datos y el esquema.</span><span class="sxs-lookup"><span data-stu-id="0a433-114">Specify the Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="0a433-115">En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Build Script** (Compilar script).</span><span class="sxs-lookup"><span data-stu-id="0a433-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="0a433-116">En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Submit Script** (Enviar script).</span><span class="sxs-lookup"><span data-stu-id="0a433-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="0a433-117">Si no se ha conectado a su suscripción de Azure, se le pedirá que especifique sus credenciales de la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a433-117">If you haven't connected to your Azure subscription, you will be prompted to enter your Azure account credentials.</span></span>
11. <span data-ttu-id="0a433-118">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="0a433-118">Click **Submit**.</span></span> <span data-ttu-id="0a433-119">Los resultados del envío y el vínculo del trabajo están disponibles en la ventana de resultados cuando se completa el envío.</span><span class="sxs-lookup"><span data-stu-id="0a433-119">Submission results and job link are available in the Results window when the submission is completed.</span></span>
12. <span data-ttu-id="0a433-120">Haga clic en el botón **Actualizar** para ver el estado del trabajo más reciente y actualizar la pantalla.</span><span class="sxs-lookup"><span data-stu-id="0a433-120">Click the **Refresh** button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="0a433-121">**Para ver la salida**:</span><span class="sxs-lookup"><span data-stu-id="0a433-121">**To see the output**</span></span>

1. <span data-ttu-id="0a433-122">En el **Explorador de servidores**, expanda **Azure**, **Data Lake Analytics**, su cuenta de Data Lake Analytics y **Cuentas de almacenamiento**, haga clic con el botón derecho en el almacén predeterminado y, finalmente, haga clic en **Explorador**.</span><span class="sxs-lookup"><span data-stu-id="0a433-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="0a433-123">Expanda Ejemplos, expanda Salidas y, finalmente, haga doble clic en **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="0a433-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="0a433-124">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="0a433-124">See also</span></span>
* [<span data-ttu-id="0a433-125">Introducción a Análisis de Data Lake mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a433-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="0a433-126">Introducción a Análisis de Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0a433-126">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0a433-127">Uso de Data Lake Tools for Visual Studio para desarrollar aplicaciones de U-SQL</span><span class="sxs-lookup"><span data-stu-id="0a433-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
