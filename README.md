![](/assets/smart_invs.png)

## SmartInvs

SmartInvs is a modern API for easily using inventories with Bukkit to make awesome GUIs. This book contains a guide on how to use this API to create your own amazing GUIs!

_This API requires Java 8 to work._

---

### Features

* Inventories of any type \(workbench, chest, furnace, ...\)
* Customizable size when possible \(chest, ...\)
* Custom titles
* Allows to prevent the player from closing its inventory
* Custom listeners for the event related to the inventory
* Iterator for inventory slots
* Page system
* Util methods to fill an inventory's row/column/borders/...
* Actions when player clicks on an item
* Update methods to edit the content of the inventory every tick

### Usage
To use the SmartInvs API, either:
- Put it in the `plugins` folder of your server, add it to your dependencies in your plugin.yml (e.g. `depend: [SmartInvs]`) and add it to the dependencies in your IDE.
- Put it inside your plugin jar, initialize an `InventoryManager` in your plugin (don't forget to call the `init()` method), and add a `.manager(invManager)` to your SmartInventory Builders.

You can download the latest version on the [Releases page](https://github.com/MinusKube/SmartInvs/releases) on Github.

You can also use a build system:
#### Gradle
```gradle
repositories {
    mavenCentral()
}

dependencies {
    compile 'fr.minuskube.inv:smart-invs:1.1.3'
}
```

#### Maven
```xml
<dependency>
  <groupId>fr.minuskube.inv</groupId>
  <artifactId>smart-invs</artifactId>
  <version>1.1.3</version>
</dependency>
```

### Preview

Here is a simple preview of an inventory.

```java
public class SimpleInventory implements InventoryProvider {

    public static final SmartInventory INVENTORY = SmartInventory.builder()
            .id("myInventory")
            .provider(new SimpleInventory())
            .size(3, 9)
            .title(ChatColor.BLUE + "My Awesome Inventory!")
            .build();

    private final Random random = new Random();

    @Override
    public void init(Player player, InventoryContents contents) {
        contents.fillBorders(ClickableItem.empty(new ItemStack(Material.STAINED_GLASS_PANE)));

        contents.set(1, 1, ClickableItem.of(new ItemStack(Material.CARROT_ITEM),
                e -> player.sendMessage(ChatColor.GOLD + "You clicked on a potato.")));

        contents.set(1, 7, ClickableItem.of(new ItemStack(Material.BARRIER),
                e -> player.closeInventory()));
    }

    @Override
    public void update(Player player, InventoryContents contents) {
        int state = contents.property("state", 0);
        contents.setProperty("state", state + 1);
        
        if(state % 5 != 0)
            return;

        short durability = (short) random.nextInt(15);

        ItemStack glass = new ItemStack(Material.STAINED_GLASS_PANE, 1, durability);
        contents.fillBorders(ClickableItem.empty(glass));
    }

}
```

And there is the result:

![](/assets/444ecfe1e103b.gif)

If we click on the carrot, we receive the message `You clicked on a potato`,
and if we click on the barrier, the inventory is closed.

### Useful links
The source code is available on [Github](https://github.com/MinusKube/SmartInvs)!
If you have some issues with the API, please [open an issue](https://github.com/MinusKube/SmartInvs/issues) on Github.

<hr>