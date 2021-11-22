#### jetpack-compose-training-summary-notes
-composable functions are what give the app the UI part  
-`setContent` defines the app layout and its where we call the *composable functions*  
-*composable functions* can only be called from composable functions  
-functions in jetpack compose start with CAPITAL LETTERS eg **`AllertMessageCard`**  
-to enable a function UI to show in the live AS preview you need to add `@Preview` to the function and `@Composable` as well. The *composable* function(s) MUST pass all the default parametters to show   
-To show the background color to the app, we need to add `ProjectNameTheme{}` and call the UI function in the the body. passing `@Preview(showBackground=true)` also does the same  
##Layouts  
in compose, we build UI hierarchy by calling composable functions inside other composable functions  
modifiers are used in styling individual elements like rows children, columns and Image resources etc  
##### Material design  
To implement Material components in compose, we need to wrap the composable function with the **`ApplicationNameTheme{}`** added in both the preview and setContent  
Material is built around **Color**,**Typography** and **Shape**  
  

Never let a composable update shared object, observable or  read/write to **sharedprefferences** *(the 3 are called side-effects)* this can be done in the background and then pass the value, This makes the fun fast.  
##### Note
1. Composable functions can execute in any order.
2. Composable functions can execute in parallel.
3. Recomposition skips as many composable functions and lambdas as possible.
4. Recomposition is optimistic and may be canceled.
5. A composable function might be run quite frequently, as often as every frame of an animation.  

executing all composable functions or lambdas should be side-effect free. When you need to perform a side-effect, trigger it from a callback.  
Recomposition is optimistic, which means Compose expects to finish recomposition before the parameters change again. If a parameter does change before recomposition finishes, Compose might cancel the recomposition and restart it with the new parameter.  
If your composable function needs data, it should define parameters for the data. You can then move expensive work to another thread, outside of composition, and pass the data to Compose using `mutableStateOf` or `LiveData`.  
*Modifiers* tell a UI how to layout, display or behave within its parent layout.  
*by* keyword in **remember** is used instead of the `=`. This is a property delegate that saves you from typing `.value` every time.  
**State hoisting** is putting a *state* that is modified by many functions under one ancestor. This reduces state duplication and code easier for testing. States that dont need to be controlled/edited by parents should not be hoisted.  
In Compose you *don't hide UI elements*. Instead, you simply don't add them to the composition, so they're not added to the UI tree that Compose generates. You do this with simple conditional Kotlin logic.  
**Callbacks** are functions passed as functions arguments.  
`parameters` are what act as *placeholders for values to go to a function when creating it*, `argumemnts` are *what you pass when you call the function*.  
In its basic usage, the `LazyColumn` API provides an `items` element within its scope, where individual item rendering logic is written. Make sure you import `androidx.compose.foundation.lazy.items` as Android Studio will pick a different items function by default.  
*LazyColumn doesn't recycle its children like RecyclerView. It emits new Composables as you scroll through it and is still performant, as emitting Composables is relatively cheap compared to instantiating Android Views.*  
Instead of using `remember` you can use `rememberSaveable`. This will save each state surviving configuration changes (such as **rotations**) and **process death**.  
Any animation created with `animate*AsState` is interruptible. This means that if the target value changes in the middle of the animation, `animate*AsState` restarts the animation and points to the new value.  
### Layouts in Jetpack Compose  
By convention, a composable `modifier` is specified as the first optional parameter of a function. This enables you to specify a modifier on a composable without having to name all parameters. e.g `modifier: Modifier = Modifier` If you're creating your own composable, consider having a modifier as a parameter, default it to `Modifier` (i.e. empty modifier that doesn't do anything) and apply it to the root composable of your function.  
Be mindful when chaining modifiers as the order matters. As they're concatenated into a single argument, the order affects the final result.  
e.g if padding was applied before the clickable modifier in a Row layout you will have not all of the area clickable because you told *"apply padding and then make the remaining place clickable"*-padding is excluded form the click. If we apply the padding modifier after the clickable one then the padding is included in the clickable area:  
#### Slot APIs  
Slots leave an empty space in the UI for the developer to fill as they wish.  
Compose uses Slots heavily in more complex components such as the Top App Bar.  
When building your own composables, you can use the `Slots API pattern` to make them more reusable.  
Scaffold allows you to implement a UI with the basic Material Design layout structure. It provides slots for the most common top-level Material components such as TopAppBar, BottomAppBar, FloatingActionButton and Drawer. With Scaffold, you make sure these components will be positioned and work together correctly.  
**LazyColumn** in Jetpack Compose is the equivalent of RecyclerView in Android Views.  
LazyColumn renders only the visible items on screen, allowing performance gains and doesn't need to `scroll` modifier.
ConstraintLayout can help you place composables relative to others on the screen and is an alternative to using multiple Rows, Columns and Boxes. ConstraintLayout is useful when implementing larger layouts with more complicated alignment requirements.  
By default, the children of ConstraintLayout will be allowed to choose the size they need to wrap their content. For example, this means that a Text is able to go outside the screen bounds when the text is too long:  
At its core, state in an application is any value that can change over time. This is a very broad definition, and encompases everything from a Room database to a variable on a class.  
A stateless composable is a composable that cannot directly change any state.  
State hoisting is a pattern of moving state up to the viewModel to make a component stateless.  
to create a lambda function in kotlin, we use the val/var keyword but not the fun keyword  
it is used as a placeholder parameter for lambda function.  
if a lambda function does not return anything you use**`Unit`** `val printName:(String)->Unit={*it*}` `it` is used as the parameter placeholder name just incase you dont want to specify the parameter name.  
`listOf()` is an initial value to avoid possible null results before the `LiveData` is initialized, if it wasn't passed items would be `List<TodoItem>?` which is nullable.  
`by` is the property delegate syntax in Kotlin, it lets us automatically unwrap the `State<List<TodoItem>>` from `observeAsState` into a regular `List<TodoItem>`  
`observeAsState` observes a `LiveData` and returns a `State` object that is updated whenever the `LiveData` changes.  
It will automatically stop observing when the composable is removed from composition.  
A *stateful* composable is a composable that owns a piece of `state` that it can change over time.  
`LocalContentColor` gives you the preferred color for content such as Icons and Typography. It is changed by composables such as `Surface` that draw a background.  
**Recomposition** is the process of calling composables again with new inputs to update the compose tree.  
When Compose runs composition the first time it builds a tree of every composable that was called. Then, during recomposition, updates the tree with the new composables that get called.  
A side-effect is any changes that's visible outside of the execution of a composable function.  
Recomposing a composable should be side-effect free.  
`remember` gives a composable function memory.
A value computed by `remembe`r will be stored in the composition tree, and only be recomputed if the *keys* to remember change.
You can think of `remember` as giving storage for a single object to a function the same way a `private val` property does in an object.  
Values remembered in composition are forgotten as soon as their calling composable is removed from the tree. They will also be re-initialized if the calling composable moves in the tree. You can cause this in the *`LazyColumn`* by removing items at the top.  
An **idempotent** composable always produces the same result for the same inputs and has no side-effects on recomposition. *Composables should be idempotent to support* recomposition.  
When adding memory to a composable, always ask yourself "will some caller reasonably want to control this?"  
If the answer is **yes**, make a parameter instead.  
If the answer is **no**, keep it as a local variable.  
`Remember` stores values in the Composition, and will forget them if the composable that called `remember` is removed.
This means you shouldn't rely upon `remember` to store important things inside of composables that add and remove children such as `LazyColumn`.
For example, animation state for a short animation is safe to remember in a child of LazyColumn, but a Todo task's completion would be forgotten on scroll if remembered here.  
`TextField` is the compose equivalent to Material's `EditText`  
`TextField` in compose is a stateless composable meaning it displays whatever you tell it to and issues events when the user types.  
Built-in composables are designed for unidirectional data flow. Most built-in composables provide at least one stateless version for each API. Compared to the View system, the built-in composables provide an option without internal state for stateful UI such as editable text. This avoids duplicated state between your application and the component. For example, it's possible in Compose to hoist the state for a `Checkbox` to a server-based API with no duplicated state.  
A `stateful` composable is a composable that owns a piece of state that it can change over time.  
You declare a MutableState object in a composable three ways:
1. `val state = remember { mutableStateOf(default) }`
2. `var value by remember { mutableStateOf(default) }`
3. `val (value, setValue) = remember { mutableStateOf(default) }`
When creating `State<T>` (or other stateful objects) in composition, it's important to remember it. Otherwise it will be re-initialized every composition.  
`MutableState<T>` similar to `MutableLiveData<T>`, but integrated with the compose runtime. Since it's observable, it will tell compose whenever it's updated so compose can recompose any composables that read it.  
State hoisting is a pattern of moving state up to make a component stateless.
When applied to composables, this often means introducing two parameters to the composable.
There is no "visibility" property in compose. Since compose can dynamically change the composition, you do not need to set visibility gone. Instead, remove composables from the composition.  
To handle work with the keyboard, TextField provides two parameters:
1. keyboardOptions - used to enable showing the Done IME action
2. keyboardActions - used to specify the action to be triggered in response to specific IME actions triggered - in our case, once Done is pressed, we want submit to be called and the keyboard to be hidden.  
When hoisting state, there are three rules to help you figure out where it should go
1. State should be hoisted to at least the lowest common parent of all composables that use the state (or read)
2. State should be hoisted to at least the highest level it may be changed (or modified)
3. If two states change in response to the same events they should be hoisted together
You can hoist state higher than these rules require, but underhoisting state will make it difficult or impossible to follow unidirectional data flow.  
`LazyColumn` is for displaying large lists of items.
It only composes the items currently on the screen, and disposes of them as soon as they leave. Unlike RecyclerView it doesn't need to do any recycling – compose handles the creation of new composables in a more efficient manner.  
#### Jetpack Compose Navigation  
The `NavController` is the central component when using Navigation in Compose; it keeps track of back stack entries, moves the stack forward, enables back stack manipulation, and navigating between screen states. Because NavController is central to navigation it has to be created first in order to navigate to destinations.  
Primary is your main brand color and secondary is used to provide accents. You can supply darker/lighter variants for contrasting areas. Background and surface colors are used for containers holding components which notionally live on a "surface" in your application.  
`App Bars` use `h6` style by default, Buttons use, err, `button` he Material type scale generator tool can help you to build your type scale.  
The core element for implementing theming in Jetpack Compose is the MaterialTheme composable. Placing this composable in your compose hierarchy allows you to specify your customisations to color, type and shapes for all components within it.  
`Color` has a number of useful methods on it such as copy allowing you to create a new color with different alpha/red/green/blue values.  
You can use the LocalContentColor CompositionLocal to retrieve the color which contrasts with the current background:  
When setting the color of any elements, prefer using a Surface to do this as it sets an appropriate content color CompositionLocal value, be wary of direct Modifier.background calls which do not set an appropriate content color.  
Often we want to emphasize or deemphasize content to communicate importance and provide visual hierarchy. Material Design recommends employing different levels of opacity to convey these different importance levels.

Jetpack Compose implements this via LocalContentAlpha. You can specify a content alpha for a hierarchy by providing a value for this CompositionLocal. Child composables can use this value, for example Text and Icon by default use the combination of LocalContentColor adjusted to use LocalContentAlpha. Material specifies some standard alpha values ( high, medium, disabled) which are modelled by the ContentAlpha object. Note that MaterialTheme defaults LocalContentAlpha to ContentAlpha.high.  
Material design suggests avoiding large areas of bright colors in dark theme. A common pattern is to color a container primary color in light theme and surface color in dark themes; many components use this strategy by default e.g. App Bars and Bottom Navigation. To make this easier to implement, Colors offers a primarySurface color which provides exactly this behaviour and these components use by default.  
Just like with colors, it's best to retrieve TextStyles from the current theme, encouraging you to use a small, consistent set of styles and making them more maintainable. MaterialTheme.typography retrieves the Typography instance set in your MaterialTheme composable, enabling you to use the styles you defined:  
If you need to apply multiple styles to some text, then you can use the AnnotatedString class to apply markup, adding SpanStyles to a range of text. You can either add these dynamically or use the DSL syntax to create content:  
You can of course use shapes yourself when creating your own components by using composables or Modifiers which accept shapes e.g. Surface, Modifier.clip, Modifier.background, Modifier.border etc.  
