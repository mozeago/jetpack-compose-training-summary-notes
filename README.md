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














