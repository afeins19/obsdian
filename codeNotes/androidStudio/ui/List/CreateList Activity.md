
# CreateList (class:AppCompatActivity)
```Kotlin 
class CreateList : AppCompatActivity(), ItemListener { 
	override fun onCreate(SavedInstanceState: Bundle?){
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_create_list)
		...
	}
}
```
- activity...(Listens for and Updates the UI based on internal logic and user interactions)
- implements the ItemListener Interface
- **onCreate** - entry point for the activity, this activity is called when the activity is first created 
# ItemAdapter (Interface)
```Kotlin 
itemAdapter = ItemAdapter(mutableListOf(), this)
```
- instance of the ItemAdapter Interface 
- bridge between internal list of items and the recycler view 

# ItemListener (Interface)
this is an interface thats probably built-in to kotlin (idrk) and we implement it in createList
```Kotlin 
// class decleration implements this interface
class CreateList : AppCompatActivity(), ItemListener
```

## overRiding ItemListener's methods
- we override the default methods of itemListener to create the behavior we want for our app. Specifically, when onItemAdd or onItemDelete is called, it tells the viewModel to make changes to the list containing our items (the raw data)
```kotlin 
override fun onItemAdd(itemName: String) {  
    viewModel.addItem(itemName)  
}  
  
override fun onItemDelete(position: Int) {  
    viewModel.deleteItem(position)  
}
```
