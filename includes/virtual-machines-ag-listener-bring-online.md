1. <span data-ttu-id="72e22-101">En el Administrador de clústeres de conmutación por error, expanda **Roles** y, a continuación, resalte el grupo de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="72e22-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="72e22-102">En hello **recursos** pestaña, haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="72e22-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="72e22-103">Haga clic en hello **dependencias** ficha. Si se enumeran varios recursos, compruebe que las direcciones IP hello tienen o no AND, las dependencias.</span><span class="sxs-lookup"><span data-stu-id="72e22-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="72e22-104">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="72e22-104">Click **OK**.</span></span>

5. <span data-ttu-id="72e22-105">Haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **poner en conexión**.</span><span class="sxs-lookup"><span data-stu-id="72e22-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="72e22-106">Después de hello agente de escucha está en línea, en hello **recursos** pestaña, haga clic en grupo de disponibilidad de hello y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="72e22-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Configurar el recurso de grupo de disponibilidad de Hola](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="72e22-108">Crear una dependencia en el recurso de nombre de agente de escucha de hello (no Hola recursos nombre de dirección IP) y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="72e22-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Agregar dependencia en nombre de agente de escucha de Hola](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="72e22-110">Inicie SQL Server Management Studio y, a continuación, conecte toohello de réplica principal.</span><span class="sxs-lookup"><span data-stu-id="72e22-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="72e22-111">Vaya demasiado**alta disponibilidad de AlwaysOn** > **grupos de disponibilidad** > **\<AvailabilityGroupName\>**   >  **Agentes de escucha del grupo de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="72e22-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="72e22-112">se debe mostrar el nombre de agente de escucha de Hola que creó en el Administrador de clústeres de conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="72e22-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="72e22-113">Haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="72e22-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="72e22-114">Hola **puerto** , especifique el número de puerto de hello para el agente de escucha del grupo de disponibilidad de hello mediante el uso de hello $EndpointPort que usó anteriormente (en este tutorial, 1433 pasaba Hola valor predeterminado) y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="72e22-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

