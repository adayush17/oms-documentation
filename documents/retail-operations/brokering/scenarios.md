# Brokering Scenarios

## Scenario 1: Fulfilling Marketplace Orders from Warehouse

A retailer wants to ensure that all orders placed through various marketplaces are fulfilled exclusively from their warehouse. This scenario is common for businesses that prefer to manage marketplace orders separately due to specific logistical or contractual obligations.

### Steps to Implement

1. **Identify Marketplace Orders**
   - Marketplace orders can be identified using specific order tags from Shopify. These tags help differentiate marketplace orders from other sales channels.
   - **Order Tags:** Ensure that all orders coming from marketplaces are tagged with `marketplace_sales_channel` in Shopify.

2. **Set Up Facility Groups**
   - HotWax Commerce allows retailers to create specific facility groups for different sales channels.
   - **Create Facility Group:** Set up a facility group that includes only warehouse facilities.
   - **Inventory Filter:** In the inventory filter, select the warehouse facilities to ensure only these facilities are considered for fulfillment.

3. **Configure Order Routing Rules**
   - Create specific routing rules to handle marketplace orders:
   - **Create Order Batch:** In HotWax Commerce, navigate to the order routing app and create a new order batch for marketplace orders.
   - **Order Filter:** Apply filters to select orders based on the `marketplace_sales_channel` tag. This ensures that only orders from marketplaces are included in this batch.

4. **Set Up Inventory Rules**
   - Define inventory rules to route marketplace orders to the warehouse:
   - **Create Inventory Rule:** Create an inventory rule within the newly created order batch.
   - **Select Facility Group:** Apply the previously created facility group that includes only warehouse facilities.

5. **Activate and Schedule**
   - Ensure the routing rules and order batches are activated and scheduled appropriately:
   - **Activate Inventory Rule:** Activate the inventory rule to ensure it is applied to incoming marketplace orders.
   - **Activate Order Batch:** Change the status of the order batch from `Draft` to `Active.`
   - **Schedule Routing:** Set the frequency at which the routing runs should occur to ensure timely fulfillment.

## Scenario 2: Fulfilling E-Commerce Orders from Warehouse and Stores

In this scenario, a retailer wants to prioritize fulfilling e-commerce orders from their warehouse. If the warehouse is unable to fulfill an order due to inventory constraints, the order should then be routed to retail stores for fulfillment.

### Steps to Implement

1. **Create Order Batch for E-Commerce Orders**
   - Start by creating an order batch that includes all e-commerce orders.
   - **Order Batch Creation:**
     - In HotWax Commerce, navigate to the order routing app.
     - Create a new order batch and name it `E-Commerce Orders.`

2. **Set Up Facility Groups**
   - Create two facility groups: one for warehouses and another for stores.
   - **Warehouse Facility Group:**
     - Go to Facility Groups.
     - Create a new facility group named `Warehouses.`
     - Add all warehouse facilities to this group.
   - **Store Facility Group:**
     - Go to Facility Groups.
     - Create a new facility group named `Stores.`
     - Add all retail store facilities to this group.

3. **Configure Inventory Rules**
   - Define inventory rules to ensure that orders are first checked for availability in warehouses, and if not available, then in stores.
   - **First Inventory Rule (Warehouses):**
     - Within the `E-Commerce Orders` batch, create an inventory rule.
     - Select the `Warehouses` facility group in the inventory filter.
     - Ensure that partial allocation is turned off to prioritize fulfillment from a single warehouse location.
   - **Second Inventory Rule (Stores):**
     - Create another inventory rule within the same order batch.
     - Select the `Stores` facility group in the inventory filter.
     - This rule will be applied if the warehouse cannot fulfill the order.

4. **Activate and Schedule**
   - Activate the inventory rules and the order batch to ensure proper order routing.
   - **Activate Inventory Rules:**
     - Activate both the warehouse and store inventory rules to ensure they are applied during the routing process.
   - **Activate Order Batch:**
     - Change the status of the `E-Commerce Orders` batch from `Draft` to `Active.`
   - **Schedule Routing:**
     - Set the frequency at which the routing runs should occur to ensure timely fulfillment of e-commerce orders.

## Scenario 3: Handling Peak Hours with Store Fulfillment

During peak hours, store managers need the flexibility to turn off fulfillment from their stores to manage capacity effectively. This ensures that stores are not overwhelmed and can maintain service quality.

### Steps to Implement

1. **Facility App**
   - Navigate to Facility App: Open the Facility App from the main menu.
   - Locate the Facility: Find the facility for which you need to adjust fulfillment capacity.
   - Open Facility Details Page: Click on the facility name to open the details page.
   - Adjust Fulfillment Capacity: Navigate to the fulfillment capacity card. Click on the chip and select “No Capacity” to temporarily turn off fulfillment from this facility.

2. **Fulfillment App**
   - Access Fulfillment App: Store managers can log in to the Fulfillment App.
   - Locate Fulfillment Capacity Card: Navigate to the fulfillment capacity card specific to their store.
   - Set Capacity to No Capacity: Directly control and adjust the fulfillment capacity to “No Capacity” to prevent new orders from being routed to their store during peak hours.

## Scenario 4: Setting Maximum Order Capacity for Stores

To prevent stores from being overloaded, retailers need to set a maximum order capacity. This ensures that once a store reaches its capacity, no additional orders are routed to it until the load decreases.

### Steps to Implement

1. **Set Maximum Order Capacity**
   - **Facility App:**
     - Open the Facility App and navigate to the relevant facility.
     - On the facility details page, go to the fulfillment capacity card.
     - Set the maximum number of orders that can be fulfilled from this facility.
   - **Fulfillment App:**
     - Store managers can also set the maximum order capacity via the Fulfillment App.
     - Navigate to the fulfillment capacity card and specify the maximum number of orders.

2. **Monitor Capacity**
   - Ensure the system is actively monitoring order counts. Once the limit is reached, no new orders are brokered to that facility until the order count drops below the maximum threshold.

## Scenario 5: Re-Routing Rejected Orders

If an order item is rejected due to inventory unavailability at a store, the system needs to re-route the order to another store with available inventory to ensure fulfillment.

### Steps to Implement

1. **Create Order Batch for Rejected Orders**
   - **Queue Filter Setup:** In the order batch settings, apply the queue filter and select the rejected order item queue. This filter ensures that only rejected orders are included in this batch.

2. **Create Inventory Rules**
   - **Define Re-routing Rules:** Set up inventory rules to determine the re-routing process. For example, prioritize stores with the highest inventory balance first, then by proximity.
   - **Facility Preferences:** Specify facility groups to ensure that orders are re-routed to appropriate stores based on defined criteria.

3. **Activate and Schedule**
   - **Activate Inventory Rules and Batch:** Activate the rules and the order batch to ensure they are in effect.
   - **Schedule Routing Runs:** Schedule the routing runs to occur at regular intervals, ensuring timely re-routing of rejected orders.

## Scenario 6: Proximity-Based Order Routing

Retailers want to ensure that orders are only fulfilled from facilities within a specific distance from the customer, reducing delivery times and costs.

### Steps to Implement

1. **Proximity Filter**
   - **Create Inventory Rule:** When setting up an inventory rule, select the proximity filter.
   - **Define Maximum Distance:** Specify the maximum distance (e.g., 50 miles) for order routing. This means orders will only be routed to facilities within this distance from the customer.

2. **Sort Inventory by Proximity**
   - **Proximity Sorting:** Within the inventory rule, sort the inventory allocations by proximity. This ensures that orders are fulfilled from the nearest possible facility, reducing delivery times and enhancing customer satisfaction.
   - **Inventory Balances:** Optionally, further sort by inventory balances to prioritize facilities with the highest stock levels, ensuring efficient inventory utilization and reducing the likelihood of stockouts.

## Scenario 7: Split Shipping Threshold Logic

Retailers want to implement a split shipping threshold, allowing orders to be fulfilled from multiple locations if the inventory at a single location falls below a certain threshold. This approach helps maintain adequate inventory levels for walk-in customers while ensuring timely fulfillment.

### Steps to Implement

1. **Brokering Threshold Setup**
   - **Brokering Safety Stock Filter:** When creating inventory rules in HotWax Commerce, select the brokering safety stock filter. This filter ensures that inventory is only allocated to an order from a facility if the facility has a specified minimum inventory level for the item.
   - **Define Minimum Safety Stock:** Determine the minimum safety stock level to keep in reserve for each item. For example, if the safety stock threshold is set to greater than 10, the inventory will only be allocated if the store has more than 10 units of that item available. This ensures that walk-in customers have access to sufficient stock.

2. **Partial Allocation Setup**
   - **Enable Partial Allocation:** Turn on the toggle for partial allocation within the inventory rules. This setting allows orders to be split across multiple facilities if no single location has enough inventory to fulfill the entire order.

3. **Inventory Allocation Process**
   - **Primary Check:** The routing engine first checks if any facility has inventory above the safety stock threshold.
   - **Secondary Check:** If no facility meets the threshold for all order items, the order is split and items are allocated from different locations to ensure faster fulfillment.

## Scenario 8: Managing Store Fulfillment Based on Rent Agreements

Retailers with diverse rent agreements, particularly in malls where rent may be tied to sales revenue, need to strategically manage order fulfillment to avoid high rental costs. Prioritizing stores with fixed or lower rent costs for order fulfillment can enhance profitability.

### Steps to Implement

1. **Facility Groups Setup**:
   - **Group 1: Fixed/Lower Rent Stores**:
     - Create a facility group that includes only the stores with fixed or lower rent costs. 
     - This prioritization ensures that orders are first routed to these cost-effective locations.
   - **Group 2: All Stores**:
     - Create another facility group that includes all stores, serving as a fallback to fulfill orders if the prioritized stores do not have sufficient inventory.

2. **Inventory Rules Definition**:
   - **Inventory Rule 1: Fixed/Lower Rent Stores**:
     - Set up an inventory rule that applies to the first facility group (Fixed/Lower Rent Stores).
     - This rule ensures that orders are first routed to these stores, minimizing rental costs.
   - **Inventory Rule 2: All Stores**:
     - Define a secondary inventory rule using the second facility group (All Stores).
     - This rule ensures that if the prioritized stores cannot fulfill the order, it will be routed to any store, preventing unfulfilled orders.

3. **Activation and Scheduling**:
   - **Activate Inventory Rules**:
     - Ensure both inventory rules are activated to be in effect.
   - **Schedule Brokering Runs**:
     - Schedule the brokering runs to execute these inventory rules at regular intervals, maintaining efficient order fulfillment.



## Scenario 8: Balancing Shipping Costs and Distance with Split Shipments

Retailers need to balance the cost of shipping, which is influenced by both the distance and the number of shipments. The goal is to minimize shipping costs by considering when it's more cost-effective to ship from multiple locations versus a single distant location. This scenario is particularly relevant for retailers with stores and warehouses spread across a wide geographic area.

### Steps to Implement

1. **Initial Proximity Check Without Partial Allocation:**
   
- When creating the first inventory rule, apply a proximity filter with a specified distance (e.g., 100 miles) without allowing partial allocation.
- This rule ensures that orders are fulfilled from a single location if all items are available within the specified distance, minimizing the shipping distance.

2. **Partial Shipment Within Proximity:**

- Create a second inventory rule that allows partial shipment within the same proximity filter (e.g., 100 miles).
- This rule ensures that if no single location within the specified distance has all items, the order can be split and fulfilled from multiple nearby locations.

3. **Fallback to Distant Locations Without Splitting:**

- In the third inventory rule, remove the proximity filter and disable partial shipment.
- This rule ensures that if the items are not available within the initial proximity, the entire order is shipped from a distant location that can fulfill the order completely, minimizing the number of shipments.
- Final Inventory Rule for All Locations with Partial Shipment:

4. **Include All Stores:**
- The final inventory rule includes all stores with partial shipment allowed.
- This rule ensures that if the order cannot be fulfilled completely from distant locations, it is split across all available locations to prevent unfulfilled orders.

5. **Activation and Scheduling**:
- **Activate Inventory Rules**:
   - Ensure all the inventory rules are activated to be in effect.
- **Schedule Brokering Runs**:
   - Schedule the brokering runs to execute these inventory rules at regular intervals, maintaining efficient order fulfillment.

