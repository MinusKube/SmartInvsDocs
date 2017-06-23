# Slot Iterators

Slot Iterators are an easy way to iterate through the slots of an inventory.
You can iterate horizontally or vertically.

### Create an Iterator
To create an iterator, use this method from the class `InventoryContents`:
```
newIterator(SlotIterator.Type type, int startRwo, int startColumn)
```
But it will just create a new iterator without saving it anywhere, it can be useful in some cases, but if you want to save your iterator to the inventory, use this method instead:
```
newIterator(String id, SlotIterator.Type type, int startRow, int startColumn)
```
You can put anything you want into this id, you will only use it to get and save the iterator.

### Get an Iterator
To get a previously saved iterator, use `iterator(String)` with the id of your iterator, if an iterator with this id exists, it will return it inside an `Optional`, else, it will return an empty `Optional`.
(Look at [java Optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) for further informations).

### Use an Iterator
When you have your iterator, you now probably want to use it.
Use the `set(ClickableItem)` method to set an item at the current position of the iterator.

Use `next()` to go to the next slot, if the type is `HORIZONTAL`, it will go one column forward, else if it is `VERTICAL`, it will go one row forward.
The `previous()` method does the same thing, but it goes to one column/row backward.

You can use the `get()` method to get the item on the current position, this method also returns an `Optional`.

The `row()` and the `column()` methods return the actual position of the iterator.
The `ended()` method returns `true` if the iterator is at the last slot of the inventory, and `else` if it isn't.

### Example
```java
@Override
public void init(Player player, InventoryContents contents) {
    contents.newIterator("test", SlotIterator.Type.HORIZONTAL, 1, 1);
}


private int state;

@Override
public void update(Player player, InventoryContents contents) {
    if(++state % 5 != 0)
        return;

    SlotIterator iter = contents.iterator("test").get();
    System.out.println(iter.column());

    if(iter.column() > 7)
        return;

    iter.set(ClickableItem.empty(new ItemStack(Material.WOOL, 1, (short) iter.column())))
            .next();
}
```
*(The state thing is to update our items only every 5 ticks instead of every tick)*

And this is the result, when applied to a basic chest inventory with 3 rows:

![](/assets/ad6eb1b56c816.gif)

<hr>