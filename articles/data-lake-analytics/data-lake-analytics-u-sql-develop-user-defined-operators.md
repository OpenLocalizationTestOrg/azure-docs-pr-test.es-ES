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
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="0fcf2-103">Desarrollo de operadores U-SQL definidos por el usuario (UDO)</span><span class="sxs-lookup"><span data-stu-id="0fcf2-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="0fcf2-104">Obtenga información acerca de cómo toodevelop definido por el usuario datos tooprocess de operadores en un trabajo de SQL U.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="0fcf2-105">Para instrucciones sobre cómo desarrollar ensamblados de propósito general para U-SQL, consulte [Desarrollo de ensamblados U-SQL para trabajos de Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="0fcf2-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="0fcf2-106">Definición y uso de un operador definido por el usuario en U-SQL</span><span class="sxs-lookup"><span data-stu-id="0fcf2-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="0fcf2-107">**toocreate y enviar un trabajo de SQL U**</span><span class="sxs-lookup"><span data-stu-id="0fcf2-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="0fcf2-108">En Visual Studio Hola seleccione **archivo > Nuevo > proyecto > U-SQL proyecto**.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="0fcf2-109">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-109">Click **OK**.</span></span> <span data-ttu-id="0fcf2-110">Visual Studio crea una solución con un archivo Script.usql.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="0fcf2-111">En el **Explorador de soluciones**, expanda Script.usql y haga doble clic en **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="0fcf2-112">Pegue Hola siguiente código en el archivo hello:</span><span class="sxs-lookup"><span data-stu-id="0fcf2-112">Paste hello following code into hello file:</span></span>

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
6. <span data-ttu-id="0fcf2-113">Abra **Script.usql**, y pegar Hola siguiendo script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="0fcf2-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

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
7. <span data-ttu-id="0fcf2-114">Especifique la cuenta de análisis de Data Lake hello, base de datos y esquema.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="0fcf2-115">En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Build Script** (Compilar script).</span><span class="sxs-lookup"><span data-stu-id="0fcf2-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="0fcf2-116">En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Submit Script** (Enviar script).</span><span class="sxs-lookup"><span data-stu-id="0fcf2-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="0fcf2-117">Si aún no lo ha conectado tooyour suscripción de Azure, que se van a ser solicitada tooenter sus credenciales de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="0fcf2-118">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-118">Click **Submit**.</span></span> <span data-ttu-id="0fcf2-119">Resultados de envío y de vínculo de trabajo están disponibles en la ventana de resultados de hello cuando se completa el envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="0fcf2-120">Haga clic en hello **actualizar** botón toosee hello más reciente trabajo estado y la actualización de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="0fcf2-121">**salida de hello toosee**</span><span class="sxs-lookup"><span data-stu-id="0fcf2-121">**toosee hello output**</span></span>

1. <span data-ttu-id="0fcf2-122">De **Explorador de servidores**, expanda **Azure**, expanda **análisis de Data Lake**, expanda y su cuenta de análisis de Data Lake **decuentasdealmacenamiento**, haga clic en hello almacenamiento predeterminado y, a continuación, haga clic en **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="0fcf2-123">Expanda Ejemplos, expanda Salidas y, finalmente, haga doble clic en **Drivers.csv**.</span><span class="sxs-lookup"><span data-stu-id="0fcf2-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="0fcf2-124">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="0fcf2-124">See also</span></span>
* [<span data-ttu-id="0fcf2-125">Introducción a Análisis de Data Lake mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fcf2-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="0fcf2-126">Empezar a trabajar con análisis de Data Lake con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0fcf2-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0fcf2-127">Uso de Data Lake Tools for Visual Studio para desarrollar aplicaciones de U-SQL</span><span class="sxs-lookup"><span data-stu-id="0fcf2-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
