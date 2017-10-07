---
title: "aplicación de Java aaaCompute intensiva en una máquina virtual | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se puede supervisar toocreate una máquina virtual de Azure que ejecuta una aplicación de Java de proceso intensivo que otra aplicación de Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>¿Cómo toorun un proceso intensivo de tareas en Java en una máquina virtual
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Con Azure, puede utilizar una tarea de proceso intensivo de toohandle de máquina virtual. Por ejemplo, una máquina virtual puede administrar las tareas y entregar máquinas tooclient de resultados o aplicaciones móviles. Después de leer este artículo, tendrá una descripción de cómo se puede supervisar toocreate una máquina virtual que ejecuta una aplicación de Java de proceso intensivo que otra aplicación de Java.

Este tutorial se supone que ya sabe cómo toocreate aplicaciones de consola de Java, puede importar la aplicación de Java de tooyour de bibliotecas y puede generar un archivo de Java (JAR). Se presupone que no tiene conocimiento sobre Microsoft Azure.

Aprenderá a:

* ¿Cómo toocreate una máquina virtual con un Kit de desarrollo de Java (JDK) ya instalado.
* ¿Cómo tooremotely inicie sesión en la máquina virtual de tooyour.
* ¿Cómo toocreate un servicio de bus de espacio de nombres.
* ¿Cómo toocreate una aplicación Java que realiza una tarea de proceso intensivo.
* ¿Cómo toocreate una aplicación Java que supervisa Hola progreso de la tarea de proceso intensivo de hello.
* ¿Cómo toorun Hola aplicaciones Java.
* ¿Cómo toostop Hola aplicaciones Java.

Este tutorial usará Hola problema del viajante de tarea de proceso intensivo de hello. Hola aquí te mostramos un ejemplo de Hola Java aplicación Hola proceso intensivo tarea en ejecución.

![Solucionador del problema del viajante (TSP)][solver_output]

Hola aquí te mostramos un ejemplo de Hola tarea de proceso intensivo de supervisión de aplicaciones de Java Hola.

![Cliente del problema del viajante][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate una máquina virtual
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Haga clic en **Nuevo**, **Proceso**, **Máquina virtual** y, a continuación, en **De la galería**.
3. Hola **seleccione de la imagen de máquina Virtual** cuadro de diálogo, seleccione **JDK 7 Windows Server 2012**.
   Tenga en cuenta que **Windows Server 2012 de JDK 6** está disponible si tiene aplicaciones heredadas que aún no están listo toorun en JDK 7.
4. Haga clic en **Siguiente**.
5. Hola **configuración de máquina Virtual** cuadro de diálogo:
   1. Especifique un nombre para la máquina virtual de Hola.
   2. Especifique hello toouse de tamaño de la máquina virtual de Hola.
   3. Escriba un nombre para el Administrador de Hola Hola **nombre de usuario** campo. Recuerde esta contraseña hello y nombre que pasará a continuación, se usa al registrar de forma remota en la máquina virtual de toohello.
   4. Escriba una contraseña en hello **nueva contraseña** campo y vuelva a escribirla en hello **confirmar** campo. Se trata de una contraseña de cuenta de administrador de Hola.
   5. Haga clic en **Siguiente**.
6. Hola siguiente **configuración de máquina Virtual** cuadro de diálogo:
   1. Para **servicio en la nube**, usar valor predeterminado de hello **crear un nuevo servicio de nube**.
   2. Hola valor para **nombre DNS del servicio de nube** debe ser único en cloudapp.net. Si es necesario, modifique este valor para que Azure indique que es exclusivo.
   3. Especifique una región, un grupo de afinidad o una red virtual. En este tutorial, especifique una región como **Oeste de EE. UU**.
   4. En **Cuenta de almacenamiento**, seleccione **Usar una cuenta de almacenamiento generada automáticamente**.
   5. En **Conjunto de disponibilidad**, seleccione **(Ninguno)**.
   6. Haga clic en **Siguiente**.
7. Hola final **configuración de máquina Virtual** cuadro de diálogo:
   1. Aceptar entradas de punto de conexión de hello predeterminadas.
   2. Haga clic en **Completo**.

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>registro de tooremotely en la máquina virtual de tooyour
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Haga clic en **Máquinas virtuales**.
3. Haga clic en el nombre de Hola de máquina virtual de Hola que desea toolog en.
4. Haga clic en **Conectar**.
5. Responder mensajes toohello como máquina virtual de toohello de tooconnect necesarios. Cuando se le solicite para contraseña y nombre de administrador de hello, utilice valores de hello que proporcionó cuando se creó la máquina virtual de Hola.

Tenga en cuenta que Hola funcionalidad de Service Bus de Azure requiere toobe de certificado raíz de Baltimore CyberTrust Hola instalado como parte de su JRE **cacerts** almacenar. Este certificado se incluye automáticamente en hello Java Runtime Environment (JRE) utilizado por este tutorial. Si no tiene este certificado en su JRE **cacerts** almacenar, consulte [agregando un toohello certificado almacén de certificados de entidad emisora de certificados de Java] [ add_ca_cert] para obtener información sobre cómo agregarlo (así como obtener información acerca de cómo ver los certificados de hello en el almacén de cacerts).

## <a name="how-toocreate-a-service-bus-namespace"></a>¿Cómo toocreate un servicio de bus de espacio de nombres
toobegin uso del Bus de servicio pone en cola en Azure, primero debe crear un espacio de nombres de servicio. Un espacio de nombres de servicio proporciona un contenedor con un ámbito para el desvío de recursos del Bus de servicio en la aplicación.

toocreate un espacio de nombres de servicio:

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. En el panel de navegación inferior izquierda de Hola de hello portal de Azure clásico, haga clic en **Bus de servicio, el Control de acceso y el almacenamiento en caché**.
3. En el panel superior izquierdo de Hola de hello portal de Azure clásico, haga clic en hello **Service Bus** nodo y, a continuación, haga clic en hello **New** botón.  
   ![Captura de pantalla del nodo Service Bus][svc_bus_node]
4. Hola **crear un nuevo Namespace de servicio** diálogo cuadro, escriba un **Namespace**, y, a continuación, haga clic en toomake seguro de que es único, el **Comprobar disponibilidad** botón.  
   ![Captura de pantalla de la creación de un nuevo espacio de nombres][create_namespace]
5. Después de asegurarse el nombre del espacio de nombres de hello está disponible, elija el país o región en la que el espacio de nombres debe hospedarse y, a continuación, haga clic en hello **crear Namespace** botón.  
   
   espacio de nombres de Hola creado aparecerá en el portal de Azure clásico de Hola y toma un tooactivate este momento. Espere hasta que el estado de hello **Active** antes de continuar con el paso siguiente de saludo.

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>Obtener credenciales de administración predeterminado de hello para el espacio de nombres de Hola
En las operaciones de administración del tooperform de orden, como la creación de una cola, en hello nuevo espacio de nombres, debe tener credenciales de administración de Hola de tooobtain para el espacio de nombres.

1. En el panel de navegación izquierdo de hello, haga clic en hello **Service Bus** nodo para mostrar lista de Hola de espacios de nombres disponibles.
   ![Captura de pantalla de los espacios de nombres disponibles][avail_namespaces]
2. Seleccione el espacio de nombres de Hola que acaba de crear desde la lista de Hola que se muestra.
   ![Captura de pantalla de lista de espacio de nombres][namespace_list]
3. Hola derecho **propiedades** panel muestra las propiedades de hello para el nuevo espacio de nombres.
   ![Captura de pantalla del panel de propiedades][properties_pane]
4. Hola **clave predeterminada** está oculto. Haga clic en hello **vista** botón credenciales de seguridad de toodisplay Hola.
   ![Captura de pantalla de la clave predeterminada][default_key]
5. Tome nota de hello **emisor predeterminado** hello y **clave predeterminada** ya que usará esta información a continuación tooperform operaciones con el espacio de nombres.

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>¿Cómo toocreate una aplicación Java que realiza una tarea de proceso intensivo
1. En el equipo de desarrollo (que no tiene la máquina virtual de toobe Hola que ha creado), descarga hello [Azure SDK para Java](https://azure.microsoft.com/develop/java/).
2. Crear una aplicación de consola de Java mediante el código de ejemplo de Hola final Hola de esta sección. En este tutorial, usaremos **TSPSolver.java** como nombre de archivo de hello Java. Modificar hello **su\_servicio\_bus\_espacio de nombres**, **su\_servicio\_bus\_propietario**y **su\_servicio\_bus\_clave** toouse de marcadores de posición del bus de servicio **espacio de nombres**, **emisor predeterminado** y  **Clave predeterminada** valores, respectivamente.
3. Después de codificar, hello de paquete y de exportación Hola aplicación tooa ejecutable archivo Java (JAR) requiere bibliotecas en hello generan JAR. En este tutorial, usaremos **TSPSolver.jar** como nombre de archivo JAR de hello generado.

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>¿Cómo toocreate una aplicación Java que supervisa Hola progreso de la tarea de proceso intensivo de hello
1. En el equipo de desarrollo, cree una aplicación de consola de Java con código de ejemplo de Hola final Hola de esta sección. En este tutorial, usaremos **TSPClient.java** como nombre de archivo de hello Java. Como se muestra anteriormente, modificar hello **su\_servicio\_bus\_espacio de nombres**, **su\_servicio\_bus\_propietario**, y **su\_servicio\_bus\_clave** toouse de marcadores de posición del bus de servicio **espacio de nombres**, **emisor predeterminado**y **clave predeterminada** valores, respectivamente.
2. Exportar Hola aplicación tooa JAR ejecutable y Hola de paquete requieren bibliotecas en hello generan JAR. En este tutorial, usaremos **TSPClient.jar** como nombre de archivo JAR de hello generado.

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>¿Cómo toorun Hola aplicaciones Java
Ejecutar la aplicación de proceso intensivo de hello, primera cola de hello toocreate y, a continuación, toosolve Hola viaja Saleseman problema, que agregará Hola actual mejor ruta toohello cola de service bus. Mientras Hola los aplicación de proceso intensivo es ejecutando (o posteriormente), resultados de ejecución Hola cliente toodisplay de cola de bus de servicio de Hola.

### <a name="toorun-hello-compute-intensive-application"></a>aplicación de proceso intensivo de hello toorun
1. Inicie sesión en la máquina virtual de tooyour.
2. Cree una carpeta en la que ejecutará la aplicación. Por ejemplo, **c:\TSP**.
3. Copia **TSPSolver.jar** demasiado**c:\TSP**,
4. Cree un archivo denominado **c:\TSP\cities.txt** con hello después de contenido.
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. En un símbolo del sistema, cambie los directorios tooc:\TSP.
6. Asegúrese de carpeta bin de hello JRE está en la variable de entorno PATH de Hola.
7. Necesitará cola de bus de servicio de hello toocreate antes de ejecutar permutaciones de hello TSP solver. Ejecute hello después de cola de bus de servicio de comando toocreate Hola.
   
        java -jar TSPSolver.jar createqueue
8. Hello cola una vez creada, puede ejecutar permutaciones de hello TSP solver. Por ejemplo, ejecute hello después solver de hello toorun de comando para 8 ciudades.
   
        java -jar TSPSolver.jar 8
   
   Si no especifica un número, se ejecutará en 10 ciudades. Como solver Hola encuentra rutas más cortas actuales, agregará toohello cola.

> [!NOTE]
> Hola número que especifique, se ejecutará solver hello más larga de Hola Hola mayor. Por ejemplo, si la ejecución en 14 ciudades puede tardar varios minutos, la ejecución en 15 ciudades podría tardar varias horas. Aumentar too16 o ciudades más podrían en días de tiempo de ejecución (finalmente semanas, meses y años). Esto es debido a toohello rápido aumento en número de Hola de permutaciones evaluada solver hello como Hola aumenta número de ciudades.
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>¿Cómo toorun Hola aplicación supervisión de cliente
1. Inicie sesión en la máquina de tooyour donde se ejecutará la aplicación de cliente de Hola. Esto no es necesario toobe Hola el mismo equipo que ejecuta hello **TSPSolver** aplicación, aunque puede ser.
2. Cree una carpeta en la que ejecutará la aplicación. Por ejemplo, **c:\TSP**.
3. Copia **TSPClient.jar** demasiado**c:\TSP**,
4. Asegúrese de carpeta bin de hello JRE está en la variable de entorno PATH de Hola.
5. En un símbolo del sistema, cambie los directorios tooc:\TSP.
6. Ejecutar el siguiente comando de Hola.
   
        java -jar TSPClient.jar
   
    Opcionalmente, especifique el número de Hola de toosleep de minutos entre la comprobación de cola de hello, pasando un argumento de línea de comandos. Hello período de espera predeterminado para la comprobación de cola de Hola es 3 minutos, que se usa si se pasa ningún argumento de línea de comandos demasiado**TSPClient**. Si desea toouse un valor diferente para el intervalo de suspensión de saludo, por ejemplo, un minuto, ejecute hello siguiente comando.
   
        java -jar TSPClient.jar 1
   
    Hola cliente se ejecutará hasta que ve un mensaje de la cola de "Completar". Tenga en cuenta que si ejecuta varias repeticiones de solver Hola sin ejecutar el cliente de hello, deberá a cliente de hello toorun cola de hello vacía toocompletely varias veces. Como alternativa, puede eliminar la cola de hello y, a continuación, vuelva a crearlo. cola de hello toodelete, ejecute hello siguiente **TSPSolver** (no **TSPClient**) comando.
   
        java -jar TSPSolver.jar deletequeue
   
    solver Hola se ejecutará hasta que finalice el examen de todas las rutas.

## <a name="how-toostop-hello-java-applications"></a>¿Cómo toostop Hola aplicaciones Java
Para solver hello y las aplicaciones cliente, puede presionar **Ctrl + C** tooexit si desea tooend toonormal anterior finalización.

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
