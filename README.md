# Android-practice-8-ViewModel
ViewModel : Android architecture component 1

# Overview
 - View data ownership should be seperated from `UI controller` and assigned to `ViewModel`. 
 
 - UI controllers such as activities and fragments are intended to display UI data and react to user actions like capturing input texts, but *nothing more.*
   > We shouldn't give excessive responsibility to UI controllers because we have no controll of it's lifecylces, only the Android framework does. When it's re-created, the data is lost.

 - `ViewModel` is a helper class for the UI controller. ViewModel **object is retained** during configuration changes and the data that it holds is immediately available to the next activity or fragment instance.
    > If we need to display a list of users, the resposibility for acquiring and keeping the list of users should be of ViewModel.

 - When activity or fragment is re-created, the **ViewModel instance is same** as the one that was created by the first activity.

 - When the activity is finished or fragment is detached, the ViewModel object is destroyed and `onCleared()` callback is called to clean up the resources.

## How to create ViewModel
 1. Add dependency and creat a class that extends ViewModel() class.
    > ViewModel() is an absract class that contains onCleared() method
    
 2. Create a reference to the ViewModel inside UI controller through `get(Class<T> modelClass)` method from `ViewModelProvider` class.
    ```
    class SomeFragment : Fragment() {
      private lateinit var viewModel: SomeViewModel
     
      override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): 
       View? {
        viewModel = ViewModelProvider(this).get(SomeViewModel::class.java)
        ...
     }                     
    }
    ```
    ViewModelProvider(context).get(..) will create new ViewModel object, or return an existing one if it exists. And this instance will not be destroyed as long as the scope is alive.
