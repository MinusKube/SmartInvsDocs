# Getting Started

We will see here how to create your first inventory using the SmartInvs API.

## SmartInventory Builder

First, get your `SmartInventory.Builder` item using the method `SmartInventory.builder()`,
then build your inventory with the different parameters:

| Parameter | Description | Default value |
| ------------- |:-------------:| -----:|
| id | Sets the id of the inventory, so you can use it later to check if the player's opened inventory is your custom inventory, per example. | `unknown` |
| title | Sets the title of the inventory. | Empty String |
| type | Sets the type of the inventory. | `CHEST` |
| size | Sets the rows and the columns amount of the inventory, for types supporting it, like chests. | 6 Rows, 9 Columns |
| closeable | Defines if the inventory can be closed by the player or not. | `true` |
| parent | Sets the parent of the inventory, so you can use it later to open it when the player clicks on a "Back" item, per example. | None |
| listener | Adds an event listener for the inventory. (Can be called multiple times) | None |
| provider | **(Mandatory)** Sets the content provider for this inventory. | None |

When all of your parameters are defined, use the method `build()` to create your SmartInventory. We recommend to put the inventory in a constant.

Example:
```java
public static final SmartInventory INVENTORY = SmartInventory.builder()
        .id("customInventory")
        .provider(new MyProvider())
        .size(4, 9)
        .title(ChatColor.RED + "Unclosable inventory!")
        .closeable(false)
        .build();
```
