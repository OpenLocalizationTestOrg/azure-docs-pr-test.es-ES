---
title: un servidor de Analysis Services de Azure .odc archivos tooconnect tooan aaaCreate | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un tooand de tooconnect del archivo de conexión de datos de Office obtener datos desde un servidor de Analysis Services en Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/23/2017
ms.author: owend
ms.openlocfilehash: 9c8c8df23b17f19905d7ec51af4eb63eb995045e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-office-data-connection-file"></a><span data-ttu-id="fc523-103">Creación de un archivo de conexión de datos de Office</span><span class="sxs-lookup"><span data-stu-id="fc523-103">Create an Office Data Connection file</span></span>

<span data-ttu-id="fc523-104">Información de este artículo describe cómo se puede crear un servidor de Analysis Services de Azure de conexión de datos de Office archivos tooconnect tooan desde Excel 2016 16.0.7369.2117 del número de versión o una versión anterior, o Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="fc523-104">Information in this article describes how you can create an Office Data Connection file tooconnect tooan Azure Analysis Services server from Excel 2016 version number 16.0.7369.2117 or earlier, or Excel 2013.</span></span> <span data-ttu-id="fc523-105">También se requiere un [proveedor de MSOLAP.7](analysis-services-data-providers.md) actualizado.</span><span class="sxs-lookup"><span data-stu-id="fc523-105">An updated [MSOLAP.7 provider](analysis-services-data-providers.md) is also required.</span></span>


1. <span data-ttu-id="fc523-106">Archivo de conexión de ejemplo de Hola a continuación de copiar y pegar en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="fc523-106">Copy hello sample connection file below and paste into a text editor.</span></span> 

2. <span data-ttu-id="fc523-107">En `odc:ConnectionString`, cambiar Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="fc523-107">In `odc:ConnectionString`, change hello following properties:</span></span>

    *   <span data-ttu-id="fc523-108">En `Data Source=asazure://<region>.asazure.windows.net/<servername>;` cambiar `<region>` toohello región de su servidor de Analysis Services y `<servername>` toohello nombre del servidor.</span><span class="sxs-lookup"><span data-stu-id="fc523-108">In `Data Source=asazure://<region>.asazure.windows.net/<servername>;` change `<region>` toohello region of your Analysis Services server and `<servername>` toohello name of your  server.</span></span>

    *   <span data-ttu-id="fc523-109">En `Initial Catalog=<database>;` cambiar `<database>` toohello nombre de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="fc523-109">In `Initial Catalog=<database>;` change `<database>` toohello name of your database.</span></span>

3. <span data-ttu-id="fc523-110">En `<odc:CommandText>Model</odc:CommandText>` cambiar `Model` toohello nombre del modelo o perspectiva.</span><span class="sxs-lookup"><span data-stu-id="fc523-110">In `<odc:CommandText>Model</odc:CommandText>` change `Model` toohello name of your model or perspective.</span></span> 

4. <span data-ttu-id="fc523-111">Guardar archivo de hello con un `.odc` toohello extensión C:\Users\\*nombre de usuario*\Documents\My carpeta de orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="fc523-111">Save hello file with an `.odc` extension toohello C:\Users\\*username*\Documents\My Data Sources folder.</span></span>

5. <span data-ttu-id="fc523-112">Haga clic en el archivo de hello y, a continuación, haga clic en **abierto en Excel**.</span><span class="sxs-lookup"><span data-stu-id="fc523-112">Right-click hello file, and then click **Open in Excel**.</span></span> <span data-ttu-id="fc523-113">O en Excel, en hello **datos** la cinta de opciones, haga clic en **las conexiones existentes**, seleccione el archivo y, a continuación, haga clic en **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="fc523-113">Or in Excel, on hello **Data** ribbon, click **Existing Connections**, select your file, and then click **Open**.</span></span>



<span data-ttu-id="fc523-114">**Archivo de conexión de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="fc523-114">**Sample connection file**</span></span>
```
<html xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns="http://www.w3.org/TR/REC-html40">

<head>
<meta http-equiv=Content-Type content="text/x-ms-odc; charset=utf-8">
<meta name=ProgId content=ODC.Cube>
<meta name=SourceType content=OLEDB>
<meta name=Catalog content="Database">
<meta name=Table content=Model>
<title>AzureAnalysisServicesConnection</title>
<xml id=docprops><o:DocumentProperties
  xmlns:o="urn:schemas-microsoft-com:office:office"
  xmlns="http://www.w3.org/TR/REC-html40">
  <o:Name>SampleAzureAnalysisServices</o:Name>
 </o:DocumentProperties>
</xml><xml id=msodc><odc:OfficeDataConnection
  xmlns:odc="urn:schemas-microsoft-com:office:odc"
  xmlns="http://www.w3.org/TR/REC-html40">
  <odc:Connection odc:Type="OLEDB">
   <odc:ConnectionString>Provider=MSOLAP.7;Data Source=asazure://<region>.asazure.windows.net/<servername>;Initial Catalog=<database>;</odc:ConnectionString>
   <odc:CommandType>Cube</odc:CommandType>
   <odc:CommandText>Model</odc:CommandText>
  </odc:Connection>
 </odc:OfficeDataConnection>
</xml>
<style>
<!--
    .ODCDataSource
    {
    behavior: url(dataconn.htc);
    }
-->
</style>
 
</head>

<body onload='init()' scroll=no leftmargin=0 topmargin=0 rightmargin=0 style='border: 0px'>
<table style='border: solid 1px threedface; height: 100%; width: 100%' cellpadding=0 cellspacing=0 width='100%'> 
  <tr> 
    <td id=tdName style='font-family:arial; font-size:medium; padding: 3px; background-color: threedface'> 
      &nbsp; 
    </td> 
     <td id=tdTableDropdown style='padding: 3px; background-color: threedface; vertical-align: top; padding-bottom: 3px'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td id=tdDesc colspan='2' style='border-bottom: 1px threedshadow solid; font-family: Arial; font-size: 1pt; padding: 2px; background-color: threedface'>

      &nbsp; 
    </td> 
  </tr> 
  <tr> 
    <td colspan='2' style='height: 100%; padding-bottom: 4px; border-top: 1px threedhighlight solid;'> 
      <div id='pt' style='height: 100%' class='ODCDataSource'></div> 
    </td> 
  </tr> 
</table> 

  
<script language='javascript'> 

function init() { 
  var sName, sDescription; 
  var i, j; 
  
  try { 
    sName = unescape(location.href) 
  
    i = sName.lastIndexOf(".") 
    if (i>=0) { sName = sName.substring(1, i); } 
  
    i = sName.lastIndexOf("/") 
    if (i>=0) { sName = sName.substring(i+1, sName.length); } 

    document.title = sName; 
    document.getElementById("tdName").innerText = sName; 

    sDescription = document.getElementById("docprops").innerHTML; 
  
    i = sDescription.indexOf("escription>") 
    if (i>=0) { j = sDescription.indexOf("escription>", i + 11); } 

    if (i>=0 && j >= 0) { 
      j = sDescription.lastIndexOf("</", j); 

      if (j>=0) { 
          sDescription = sDescription.substring(i+11, j); 
        if (sDescription != "") { 
            document.getElementById("tdDesc").style.fontSize="x-small"; 
          document.getElementById("tdDesc").innerHTML = sDescription; 
          } 
        } 
      } 
    } 
  catch(e) { 

    } 
  } 
</script> 

</body> 
 
</html>

```



