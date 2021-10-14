# jetpack-compose-training-summary-notes
-composable functions are what give the app the UI part  
-`setContent` defines the app layout and its where we call the *composable functions*  
-*composable functions* can only be called from composable functions  
-functions in jetpack compose start with CAPITAL LETTERS eg **`AllertMessageCard`**  
-to enable a function UI to show in the live AS preview you need to add `@Preview` to the function and `@Composable` as well. The *composable* function(s) MUST pass all the default parametters to show   
-To show the background color to the app, we need to add `ProjectNameTheme{}` and call the UI function in the the body. passing `@Preview(showBackground=true)` also does the same  
##Layouts  





