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










