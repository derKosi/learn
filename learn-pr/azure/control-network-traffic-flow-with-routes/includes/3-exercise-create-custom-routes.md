As you implement your security strategy, you want to control how network traffic is routed across your Azure infrastructure.

In the following exercise, you use a network virtual appliance (NVA) to help secure and monitor traffic. You want to ensure communication between front-end public servers and internal private servers is always routed through the appliance.

You configure the network so that all traffic flowing from a public subnet to a private subnet will be routed through the NVA. To make this flow happen, you create a custom route for the public subnet to route this traffic to a perimeter-network subnet. Later, you deploy an NVA to the perimeter-network subnet.

:::image type="content" source="../media/3-virtual-network-subnets-route-table.svg" alt-text="Diagram of virtual network, subnets, and route table.":::

In this exercise, you create the route table, custom route, and subnets. You'll then associate the route table with a subnet.

[!INCLUDE[](../../../includes/azure-optional-exercise-subscription-note.md)]

[!INCLUDE[](../../../includes/azure-optional-exercise-create-resource-group-note.md)]

> [!NOTE]
> Throughout this exercise, replace **myResourceGroupName** in the examples with the name of an existing resource group, or the name of the resource group that you created for this exercise.

## Create a route table and custom route

The first task is to create a new routing table and then add a custom route for all traffic intended for the private subnet.

> [!NOTE]
> You might get an error that reads: *This command is implicitly deprecated*. Please ignore this error for this learning module. We're working on it!

1. Open the [Azure Cloud Shell](https://shell.azure.com/), select **Settings**, then select **Go to Classic version**.

1. In Azure Cloud Shell, run the following command to create a route table. Replace **myResourceGroupName** with the name of your resource group.

    ```azurecli
        az network route-table create \
            --name publictable \
            --resource-group "myResourceGroupName" \
            --disable-bgp-route-propagation false
    ```

1. Run the following command in Cloud Shell to create a custom route:

    ```azurecli
        az network route-table route create \
            --route-table-name publictable \
            --resource-group "myResourceGroupName" \
            --name productionsubnet \
            --address-prefix 10.0.1.0/24 \
            --next-hop-type VirtualAppliance \
            --next-hop-ip-address 10.0.2.4
    ```

## Create a virtual network and subnets

The next task is to create the **vnet** virtual network and the three subnets you need: **publicsubnet**, **privatesubnet**, and **dmzsubnet**.

1. Run the following command to create the **vnet** virtual network and the **publicsubnet** subnet:

    ```azurecli
        az network vnet create \
            --name vnet \
            --resource-group "myResourceGroupName" \
            --address-prefixes 10.0.0.0/16 \
            --subnet-name publicsubnet \
            --subnet-prefixes 10.0.0.0/24
    ```

1. Run the following command in Cloud Shell to create the **privatesubnet** subnet:

    ```azurecli
        az network vnet subnet create \
            --name privatesubnet \
            --vnet-name vnet \
            --resource-group "myResourceGroupName" \
            --address-prefixes 10.0.1.0/24
    ```

1. Run the following command to create the **dmzsubnet** subnet:

    ```azurecli
        az network vnet subnet create \
            --name dmzsubnet \
            --vnet-name vnet \
            --resource-group "myResourceGroupName" \
            --address-prefixes 10.0.2.0/24
    ```

1. You should now have three subnets. Run the following command to show all of the subnets in the **vnet** virtual network:

    ```azurecli
        az network vnet subnet list \
            --resource-group "myResourceGroupName" \
            --vnet-name vnet \
            --output table
    ```

## Associate the route table with the public subnet

The final task in this exercise is to associate the route table with the **publicsubnet** subnet.

Run the following command to associate the route table with the public subnet.

```azurecli
    az network vnet subnet update \
        --name publicsubnet \
        --vnet-name vnet \
        --resource-group "myResourceGroupName" \
        --route-table publictable
```
