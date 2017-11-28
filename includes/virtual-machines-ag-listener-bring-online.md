1. <span data-ttu-id="60f27-101">En el Administrador de clústeres de conmutación por error, expanda **Roles** y, a continuación, resalte el grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="60f27-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="60f27-102">En la pestaña **Recursos**, haga clic con el botón derecho en el nombre del agente de escucha y, a continuación, haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="60f27-102">On the **Resources** tab, right-click the listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="60f27-103">Haz clic en la pestaña **Dependencias** .</span><span class="sxs-lookup"><span data-stu-id="60f27-103">Click the **Dependencies** tab.</span></span> <span data-ttu-id="60f27-104">Si aparecen varios recursos, compruebe que las direcciones IP tienen dependencias OR y no AND.</span><span class="sxs-lookup"><span data-stu-id="60f27-104">If multiple resources are listed, verify that the IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="60f27-105">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="60f27-105">Click **OK**.</span></span>

5. <span data-ttu-id="60f27-106">Haga clic con el botón derecho en el nombre del agente de escucha y luego haga clic en **Poner en línea**.</span><span class="sxs-lookup"><span data-stu-id="60f27-106">Right-click the listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="60f27-107">Una vez que el agente de escucha está en línea, en la pestaña **Recursos**, haga clic con el botón derecho en el grupo de disponibilidad y haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="60f27-107">After the listener is online, on the **Resources** tab, right-click the availability group, and then click **Properties**.</span></span>
   
    ![Configurar el recurso del grupo de disponibilidad](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="60f27-109">Cree una dependencia en el recurso del nombre del agente de escucha (no en el nombre de los recursos de dirección IP) y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="60f27-109">Create a dependency on the listener name resource (not the IP address resources name), and then click **OK**.</span></span>
   
    ![Agregar dependencias en el nombre del agente de escucha](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="60f27-111">Abra SQL Server Management Studio y conéctese a la réplica principal.</span><span class="sxs-lookup"><span data-stu-id="60f27-111">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

9. <span data-ttu-id="60f27-112">Vaya a **Alta disponibilidad AlwaysOn** > **Grupos de disponibilidad** > **\<nombre del grupo de disponibilidad\>** > **Agentes de escucha del grupo de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="60f27-112">Go to **AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="60f27-113">Debe mostrarse el nombre del agente de escucha que creó en el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="60f27-113">The listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="60f27-114">Haga clic con el botón derecho en el nombre del agente de escucha y luego en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="60f27-114">Right-click the listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="60f27-115">En el cuadro de texto **Puerto**, especifique el número del puerto del agente de escucha del grupo de disponibilidad mediante el parámetro $EndpointPort usado anteriormente (en este tutorial, el valor predeterminado era 1433) y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="60f27-115">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort that you used earlier (in this tutorial, 1433 was the default), and then click **OK**.</span></span>

