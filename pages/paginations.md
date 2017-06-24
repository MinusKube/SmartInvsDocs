# Paginations

With the pagination system of SmartInvs, you can easily create pages for your inventories.

### Get a Pagination
To get the Pagination object of your `InventoryContents`, simply call its `pagination()` method.

### Use a Pagination
Now, we'll see how to use this pagination in our inventory.

First, we need to set some informations for our pagination, we'll use the `setItems(ClickableItem...)` method to set all our items to the object.

Then we can also use the `setItemsPerPage(int)` method to tell to our pagination how many items we want per page, the default value is `5`.

Okay, now, let's see the available getters:

| Method Name   | Description  |
| ------------- |:-------------|
| getPage       | Returns the actual page |
| getPageItems  | Returns the items for the actual page, the returned array will always be of the size of the pagination's items per page |
| isFirst       | Returns true if the actual page is the first page, else it returns false   |
| isLast        | Returns true if the actual page is the first page for the given items, else it returns false |

Then to change the actual page, several methods are availables:
* `first()` to set the page to the first
* `last()` to set the page to the last non-empty
* `previous()` to go one page backward, if possible
* `next()` to go one page forward, if possible

And finally, to add our items to our inventory, we can either use the `getPageItems()` method and put the items manually, or we can use `addToIterator(SlotIterator)` to automatically add our items from a Slot Iterator.

### Example
```java
@Override
public void init(Player player, InventoryContents contents) {
    Pagination pagination = contents.pagination();

    ClickableItem[] items = new ClickableItem[22];

    for(int i = 0; i < items.length; i++)
        items[i] = ClickableItem.empty(new ItemStack(Material.CHORUS_FRUIT, i));

    pagination.setItems(items);
    pagination.setItemsPerPage(7);

    pagination.addToIterator(contents.newIterator(SlotIterator.Type.HORIZONTAL, 1, 1));

    contents.set(2, 3, ClickableItem.of(new ItemStack(Material.ARROW),
            e -> INVENTORY.open(player, pagination.next().getPage())));
    contents.set(2, 5, ClickableItem.of(new ItemStack(Material.ARROW),
            e -> INVENTORY.open(player, pagination.previous().getPage())));
}

@Override
public void update(Player player, InventoryContents contents) {}
```

And this is the result, when applied to a basic chest inventory with 3 rows:

![](/assets/95c42f7a19e1e.gif)

<hr>