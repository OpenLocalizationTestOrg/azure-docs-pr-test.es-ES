1. En el Administrador de clústeres de conmutación por error, expanda **Roles** y, a continuación, resalte el grupo de disponibilidad.  

2. En hello **recursos** pestaña, haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **propiedades**.

3. Haga clic en hello **dependencias** ficha. Si se enumeran varios recursos, compruebe que las direcciones IP hello tienen o no AND, las dependencias.  

4. Haga clic en **Aceptar**.

5. Haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **poner en conexión**.

6. Después de hello agente de escucha está en línea, en hello **recursos** pestaña, haga clic en grupo de disponibilidad de hello y, a continuación, haga clic en **propiedades**.
   
    ![Configurar el recurso de grupo de disponibilidad de Hola](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Crear una dependencia en el recurso de nombre de agente de escucha de hello (no Hola recursos nombre de dirección IP) y, a continuación, haga clic en **Aceptar**.
   
    ![Agregar dependencia en nombre de agente de escucha de Hola](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. Inicie SQL Server Management Studio y, a continuación, conecte toohello de réplica principal.

9. Vaya demasiado**alta disponibilidad de AlwaysOn** > **grupos de disponibilidad** > **\<AvailabilityGroupName\>**   >  **Agentes de escucha del grupo de disponibilidad**.  
    se debe mostrar el nombre de agente de escucha de Hola que creó en el Administrador de clústeres de conmutación por error.

10. Haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **propiedades**.

11. Hola **puerto** , especifique el número de puerto de hello para el agente de escucha del grupo de disponibilidad de hello mediante el uso de hello $EndpointPort que usó anteriormente (en este tutorial, 1433 pasaba Hola valor predeterminado) y, a continuación, haga clic en **Aceptar**.

