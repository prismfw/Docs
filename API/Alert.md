#Prism.UI.Alert
Represents an object that modally presents an alert or confirmation dialog.  These objects are only meant to display one or two lines of text and one to three buttons; if your design requires a more advanced UI, use a **Prism.UI.Popup** instead.

####Declaration
`public class Alert : Prism.FrameworkObject`

####Inheritance Structure
* System.Object
	* Prism.FrameworkObject
		* Prism.UI.Alert

##Public Members
######Properties

###ButtonCount
Gets the number of buttons that have been added to the alert.  To add buttons to the alert, use the AddButton method.

#####Declaration
`public int ButtonCount { get; }`

--
###CancelButtonIndex
Gets or sets the zero-based index of the button that is mapped to the Escape key on desktop platforms.  This property does not have any effect on Android or iOS platforms.

#####Declaration
`public int CancelButtonIndex { get; set; }`

--
###DefaultButtonIndex
Gets or sets the zero-based index of the button that is mapped to the Enter key on desktop platforms.  This property does not have any effect on Android or iOS platforms.

#####Declaration
`public int DefaultButtonIndex { get; set; }`

--
###Message
Gets the message text for the alert.  This property is set through the constructor.

#####Declaration
`public string Message { get; }`

--
###Title
Gets the title text for the alert.  This property is set through the constructor.

#####Declaration
`public string Title { get; }`

--
######Events
None

--

######Methods

###AddButton(AlertButton button)
Adds the specified AlertButton to the alert.  Once a button is added, it cannot be removed.  You must create a new Alert if you wish to reset the buttons.  Although there is no explicit limitation on the number of buttons that can be added, many platforms will only utilize the first three and ignore any subsequent additions.  Keep this in mind when designing your alert.

#####Declaration
`public void AddButton(Prism.UI.AlertButton button)`

#####Exceptions
`System.ArgumentNullException` - Thrown when the button is a null value.

--
###Alert(string message, string title)
Constructor; initializes a new instance of the Alert class.  The message and title parameters are used to specify the message text and title text of the alert, respectively.  These values can only be set upon construction; to specify a different message or title, a new Alert instance must be created.

#####Declaration
`public Alert(string message, string title)`

--
###GetButton(int index)
Gets the button at the specified zero-based index.  If no button exists at the specified index, null will be returned.

#####Declaration
`public Prism.UI.AlertButton GetButton(int index)`

--
###Show
Modally presents the alert.  Depending on the platform, execution of the calling thread may or may not be suspended.  It is recommended that no other logic be defined after the calling of Show to avoid potential unwanted side effects.  Any and all logic responding to the selection of an alert button and the dismissal of the alert should be defined within the appropriate alert button's Action delegate.

#####Declaration
`public void Show()`
  
##Protected Members
######Properties
None

--
######Events
None

--
######Methods
###Alert(INativeAlert nativeObject)
Constructor; initializes a new instance of the Alert class and pairs it with the specified native object.  Derived classes can use this constructor if they already have a reference to the object that contains the appropriate native implementation details.  The framework will automatically pair the given object with the new Alert instance.  The type of the given object will be compared with the registered type specified by the topmost ResolveAttribute in the inheritance chain.  If they are not the same type, an exception will be thrown.

#####Declaration
`protected Alert(Prism.Native.INativeAlert nativeObject)`

#####Exceptions
`System.ArgumentException - Thrown when the native object doesn't match the type specified by the topmost ResolveAttribute in the inheritance chain.`

`System.ArgumentNullException - Thrown when a null value is given for the native object.`

--
###Alert(ResolveParameters[] resolveParameters)
Constructor; initializes a new instance of the Alert class and pairs it with a native object that is resolved from the IoC container.  Derived classes can use this constructor if they don't yet have a reference to an object that contains the appropriate native implementation details and they require an instance to be resolved from the IoC container.  The constructor will take the topmost class in the inheritance chain that is decorated with a ResolveAttribute and use the attribute to resolve the native object from the default TypeManager.  The resulting object will then be paired with the new Alert instance.  The resolveParameters, if any, are passed to the TypeManager after they are checked for invalid null values.  These values are passed to the appropriate constructor or registered initialization method of the type being resolved.  Note that these values are passed in the same order that they are provided, so it is critical to specify the parameters in the exact order that the native type's constructor or initialization method expects them.

#####Declaration
`protected Alert(Prism.ResolveParameters[] resolveParameters)`

#####Exceptions
```
Prism.TypeResolutionException - Thrown when an object could not be  
resolved from the IoC container or when the resolved object doesn't
implement the Prism.INativeAlert interface.
```

##Examples
```
var alert = new Alert("Are you sure you wish to proceed with this action?", "Are You Sure?");
alert.AddButton(new AlertButton("OK", (button) => { Application.Navigate("NextController"); }));
alert.AddButton(new AlertButton("Cancel"));
alert.Show();
```
