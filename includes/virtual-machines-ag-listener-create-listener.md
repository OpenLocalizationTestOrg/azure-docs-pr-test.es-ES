En este paso, se crea manualmente el agente de escucha del grupo de disponibilidad de hello en el Administrador de clústeres de conmutación por error y SQL Server Management Studio.

1. Abra el Administrador de clústeres de conmutación por error de nodo de Hola que hospeda la réplica principal de Hola.

2. Seleccione hello **redes** nodo y, a continuación, el nombre de red de clúster de Hola de nota. Este nombre se usa en la variable de hello $ClusterNetworkName Hola script de PowerShell.

3. Expanda el nombre del clúster de hello y, a continuación, haga clic en **Roles**.

4. Hola **Roles** panel, grupo de disponibilidad de hello contextual nombre y, a continuación, seleccione **Agregar recurso** > **punto de acceso de cliente**.
   
    ![Agregar un punto de acceso cliente para el grupo de disponibilidad](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. Hola **nombre** cuadro, cree un nombre para este nuevo agente de escucha, haga clic en **siguiente** dos veces y, a continuación, haga clic en **finalizar**.  
    No detenga el agente de escucha de Hola o recurso en línea en este momento.

6. Haga clic en hello **recursos** ficha y, a continuación, expanda el punto de acceso de cliente de Hola que acaba de crear. 
    se muestra el recurso de dirección IP de Hola para cada red de clúster en el clúster. Si se trata de una solución solo de Azure, se muestra un único recurso de dirección IP.

7. Realice una de las siguientes de hello:
   
   * tooconfigure una solución híbrida:
     
        a. Haga clic en recurso de dirección IP de Hola que corresponde la subred local de tooyour y, a continuación, seleccione **propiedades**. Observe el nombre de dirección IP de Hola y el nombre de red.
   
        b. Seleccione **Dirección IP estática**, asigne una dirección IP no utilizada y, a continuación, haga clic en **Aceptar**.
 
   * tooconfigure una solución solo de Azure:

        a. Haga clic en recurso de dirección IP de hello correspondiente tooyour subred de Azure y, a continuación, seleccione **propiedades**.
       
       > [!NOTE]
       > Si el agente de escucha de hello más adelante se produce un error toocome en línea debido a una dirección IP en conflicto seleccionada por DHCP, puede configurar una dirección IP estática válida en esta ventana de propiedades.
       > 
       > 

       b. En Hola mismo **dirección IP** ventana Propiedades, cambiar hello **nombre de dirección IP**.  
        Este nombre se usa en la variable de hello $IPResourceName de hello script de PowerShell. Si la solución abarca varias redes virtuales de Azure, repita este paso para cada recurso de dirección IP.

