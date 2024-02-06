```xml
<EditText 
	android:id="@+id/editText"
	
	android:layout_width="match_parent"
	android:layout_height="wrap_content"	
/>
```

## Attributes 
_android:text="testestest"_ - initial text in the EditText box
_android:hint="enter your name"_ - underlying hint for user (greyed out)
_android:inputType="text"_ - 

### Activity Creation (Kotlin)
```Kotlin 

```Kotlin
Class MainActivity : AppCompactActivity() {
	override fun onCreate(savedInstanceState: Bundle?){
		super.onCreate(savedInstanceState)
		setContentView(R.layout.activity_main)

		val editTextExample : EditText = findViewById(R.id.editText)

		// getting the input from edittext
		val userInput : String = editTextExample.text
		
	}
}

```