---
title: "Stream Analytics: Giro de las credenciales de inicio de sesión para entradas y salidas | Microsoft Docs"
description: "Obtenga información acerca de cómo tooupdate hello las credenciales para el análisis de transmisiones entradas y salidas."
keywords: "credenciales de inicio de sesión"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Giro de las credenciales de inicio de sesión para entradas y salidas de los trabajos de Análisis de transmisiones
## <a name="abstract"></a>Descripción breve
Análisis de transmisiones de Azure hoy no permite reemplazar las credenciales de hello en una entrada/salida mientras se ejecuta el trabajo de Hola.

Mientras que los análisis de transmisiones de Azure admiten reanudar un trabajo desde el último resultado, deseamos tooshare Hola todo el proceso para minimizar el retardo de hello entre Hola detener y a partir del trabajo de Hola y rotación de credenciales de inicio de sesión de Hola.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Parte 1: preparar el nuevo conjunto de credenciales de hello:
Esta parte es aplicable toohello después de entradas/salidas:

* Blob Storage
* Centros de eventos
* Base de datos SQL
* Almacenamiento de tablas

Para otras entradas/salidas, vaya a la Parte 2.

### <a name="blob-storagetable-storage"></a>Almacenamiento de blobs/almacenamiento de tablas
1. Vaya toohello extensión de almacenamiento en el portal de administración de Azure de hello:  
   ![graphic1][graphic1]
2. Busque utilizada por el trabajo de almacenamiento de Hola y vaya a ella:  
   ![graphic2][graphic2]
3. Haga clic en el comando de hello administrar claves de acceso:  
   ![graphic3][graphic3]
4. Entre la clave de acceso principal de Hola y Hola clave de acceso secundaria, **elegir Hola uno no utilizada por el trabajo**.
5. Presione regenerar:   
   ![graphic4][graphic4]
6. Copie la clave de hello recién generado:  
   ![graphic5][graphic5]
7. Continuar tooPart 2.

### <a name="event-hubs"></a>Centros de eventos
1. Vaya toohello extensión de Bus de servicio en el portal de administración de Azure de hello:  
   ![graphic6][graphic6]
2. Busque Hola Namespace de Bus de servicio utilizada por el trabajo y vaya a ella:  
   ![graphic7][graphic7]
3. Si el trabajo usa una directiva de acceso compartido en hello Namespace de Bus de servicio, consulte el toostep 6  
4. Vaya a toohello centros de eventos pestaña:  
   ![graphic8][graphic8]
5. Busque Hola concentrador de eventos utilizado por el trabajo y vaya a ella:  
   ![graphic9][graphic9]
6. Vaya toohello ficha configurar:  
   ![graphic10][graphic10]
7. En hello desplegable Nombre de la directiva, busque la directiva de acceso de hello compartido utilizada por el trabajo:  
   ![graphic11][graphic11]
8. Entre la clave principal de Hola y Hola clave secundaria, **elegir Hola uno no utilizada por el trabajo**.  
9. Presione regenerar:   
   ![graphic12][graphic12]
10. Copie la clave de hello recién generado:  
   ![graphic13][graphic13]
11. Continuar tooPart 2.  

### <a name="sql-database"></a>SQL Database
> [!NOTE]
> Nota: deberá tooconnect toohello servicio de base de datos de SQL. Vamos a tooshow cómo toodo esta mediante Hola experiencia de administración en Hola portal de administración de Azure, pero puede elegir toouse alguna herramienta de cliente como SQL Server Management Studio.
>
> 

1. Vaya toohello extensión de bases de datos SQL en el portal de administración de Azure de hello:  
   ![graphic14][graphic14]
2. Busque Hola utilizada por el trabajo de base de datos de SQL y **haga clic en el servidor de hello** vínculo Hola misma línea:  
   ![graphic15][graphic15]
3. Haga clic en el comando de hello administrar:  
   ![graphic16][graphic16]
4. Tipo de base de datos maestra:   
   ![graphic17][graphic17]
5. Escriba su nombre de usuario y contraseña, y haga clic en Iniciar sesión:   
   ![graphic18][graphic18]
6. Haga clic en Nueva consulta:   
   ![graphic19][graphic19]
7. Tipo de hello las siguientes consultas reemplazando < login_name > con el nombre de usuario y reemplazando <enterStrongPasswordHere> con la nueva contraseña:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Haga clic en Ejecutar:   
   ![graphic20][graphic20]
9. Volver atrás toostep 2 y esta vez haga clic en la base de datos de hello:  
   ![graphic21][graphic21]
10. Haga clic en el comando de hello administrar:  
   ![graphic22][graphic22]
11. escriba su nombre de usuario y contraseña, y haga clic en Iniciar sesión:   
   ![graphic23][graphic23]
12. Haga clic en Nueva consulta:   
   ![graphic24][graphic24]
13. Escriba hello las siguientes consultas reemplazando < nombre_usuario > con un nombre por el que quiere tooidentify este inicio de sesión en el contexto de Hola de esta base de datos (puede proporcionar Hola el mismo valor que se le asignó para < login_name >, por ejemplo) y reemplazando < login_name > por el nuevo nombre de usuario:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Haga clic en Ejecutar:   
   ![graphic25][graphic25]
15. Ahora debe proporcionar el nuevo usuario con hello mismos roles y privilegios que tenía el usuario original.
16. Continuar tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Parte 2: Hola de detención flujo de trabajo de análisis
1. Vaya toohello extensión de análisis de transmisiones en el portal de administración de Azure de hello:  
   ![graphic26][graphic26]
2. Busque su trabajo y vaya a él:   
   ![graphic27][graphic27]
3. Vaya toohello entradas ficha u Hola salidas en función de si va a rotar las credenciales en una entrada o en una salida de hello.  
   ![graphic28][graphic28]
4. Haga clic en el comando de detención de Hola y confirme el trabajo Hola se ha detenido:  
   ![graphic29][graphic29] espere hello toostop de trabajo.
5. Busque Hola entrada/salida que desee toorotate credenciales en y vaya a ella:  
   ![graphic30][graphic30]
6. Continúe tooPart 3.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Parte 3: Editar credenciales de hello en hello trabajo de análisis de transmisiones
### <a name="blob-storagetable-storage"></a>Almacenamiento de blobs/almacenamiento de tablas
1. Encontrar el campo de clave de la cuenta de almacenamiento de Hola y pegue la clave recién generada:  
   ![graphic31][graphic31]
2. Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:  
   ![graphic32][graphic32]
3. Al guardar los cambios se iniciará automáticamente una prueba de conexión ; asegúrese de que haya pasado correctamente.
4. Continúe tooPart 4.

### <a name="event-hubs"></a>Centros de eventos
1. Encontrar el campo de clave de directiva de centro de eventos de Hola y pegue la clave recién generada:  
   ![graphic33][graphic33]
2. Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:  
   ![graphic34][graphic34]
3. Una prueba de conexión se iniciará automáticamente al guardar los cambios; asegúrese de que haya pasado correctamente.
4. Continúe tooPart 4.

### <a name="power-bi"></a>Power BI
1. Haga clic en la autorización de renovación de hello:  

   ![graphic35][graphic35]
2. Obtendrá Hola después de confirmación:  

   ![graphic36][graphic36]
3. Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:  
   ![graphic37][graphic37]
4. Al guardar los cambios se iniciará automáticamente una prueba de conexión ; asegúrese de que haya pasado correctamente.
5. Continúe tooPart 4.

### <a name="sql-database"></a>SQL Database
1. Buscar campos de nombre de usuario y contraseña de Hola y pegue el conjunto de credenciales recién creado:  
   ![graphic38][graphic38]
2. Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:  
   ![graphic39][graphic39]
3. Una prueba de conexión se iniciará automáticamente al guardar los cambios; asegúrese de que haya pasado correctamente.  
4. Continúe tooPart 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Parte 4: Inicio del trabajo desde la última vez que se detuvo
1. Salir de hello entrada/salida:  
   ![graphic40][graphic40]
2. Haga clic en el comando de inicio de hello:  
   ![graphic41][graphic41]
3. Elija última hora de detención de Hola y haga clic en Aceptar:  
   ![graphic42][graphic42]
4. Continúe tooPart 5.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Parte 5: Quitar Hola anterior conjunto de credenciales
Esta parte es aplicable toohello después de entradas/salidas:

* Blob Storage
* Centros de eventos
* Base de datos SQL
* Almacenamiento de tablas

### <a name="blob-storagetable-storage"></a>Almacenamiento de blobs/almacenamiento de tablas
Repita parte 1 para la clave de acceso que se había utilizado previamente por el trabajo de Hola toorenew Hola ahora sin usar la clave de acceso.

### <a name="event-hubs"></a>Centros de eventos
Repita parte 1 de hello clave que se había utilizado previamente por el trabajo toorenew Hola clave ahora sin usar.

### <a name="sql-database"></a>SQL Database
1. Volver atrás ventana de consulta toohello parte 1 paso 7 y tipo Hola después de consulta, reemplazando < previous_login_name > con el nombre de usuario que se usó previamente por el trabajo de hello:  
   `DROP LOGIN <previous_login_name>`  
2. Haga clic en Ejecutar:   
   ![graphic43][graphic43]  

Debería obtener Hola después de confirmación: 

    Command(s) completed successfully.

## <a name="get-help"></a>Obtener ayuda
Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Pasos siguientes
* [Introducción tooAzure análisis de transmisiones](stream-analytics-introduction.md)
* [Introducción al uso de Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Escalación de trabajos de Análisis de transmisiones de Azure](stream-analytics-scale-jobs.md)
* [Referencia del lenguaje de consulta de Análisis de transmisiones de Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referencia de API de REST de administración de Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

