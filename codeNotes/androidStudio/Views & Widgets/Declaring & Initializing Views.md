the process of creating references to your UI elements so you can interact with them via kotlin

# Creating and Referencing a View
## ID Attribute
the most important attribute of any view object or view group
- allows android to uniquely identify this view 
## Example using TextView 
### Layout Creation (XML)
- this is declared in an xml file in your layout folder
```XML
activity_test.xml

<TextView
		android:id="@+id/test"
/> 
```

### Activity Creation (Kotlin)
- id must be unique and must exist in order for kotlin to find and interact with the object 
```Kotlin
Class MainActivity : AppCompactActivity() {
	override fun onCreate(savedInstanceState: Bundle?){
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_main)
	
		val sample = findViewById(R.id.test) //this find the view from the layoutfolder
		sample.setText("Howdy!")
	}
}

```
