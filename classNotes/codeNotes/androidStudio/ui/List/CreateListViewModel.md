This is the backend file which handles the apps internal representation of data. Interactions with the UI and the database are sent here. 

# Private Data Container 
```kotlin
private val _itemList = MutableLiveData<MutableList<Item>>()
```
- is the mutable list of items which will be modified as the app is used 
- this list may only be changed by CreateListViewModel and cannot be accesed from other files 

# Public Data Container
```Kotlin
```kotlin
val itemList: LiveData<MutableList<Item>> get() = _itemList
```
- this is what createListView (activity) has access to, its a read-only copy of the private itemlist 
- this ensures separation of concerns as CreateListViewModel handles data manipulation and storage and shouldnt provide access to these functions externally 

# Initialization
```kotlin
init {
	_itemList.value = mutableListOf()
}
```
- intializer that gets called when an instance of CreateListViewModel is created. It declares the itemlists initial value to an empty mutable list 

# AddItem()
```kotlin
fun addItem(itemName: String) {
    val list = _itemList.value ?: mutableListOf()
    val item = list.find { it.name == itemName }

    if (item == null) {
        list.add(Item(itemName, 1))
    } else {
        item.quantity++
    }

    _itemList.value = list
}
```
- this function adds items to the list, if the item already exists, it will just increase the quantity of that item 
- we check to see if the item already exists in the list with the find function (find { it.name == itemName})
- 