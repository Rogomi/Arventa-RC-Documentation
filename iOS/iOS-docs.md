[Back](../README.md)

# **Arventa Connect**
## Technical Documentation

### **GETTING STARTED**
Arventa Connect iOS requires Xcode 11.0 and above for development. This project uses Swift 5 as the Programming Language, Storyboard for the Interface and CocoaPods for Third Party Libraries. The app also uses SQLCipher to store offline information. The current Xcode version used for development is 12.0. The minimum iOS Version required is iOS 12.0

### **INSTALLATION AND DEVELOPMENT**
In order to start with the development, first, you will need an Apple account for development. It must be under the team MSDS.COM.AU PTY LTD. Then, open the Arventa Connect.xcworkspace under the repository root directory. If possible, do a pods repo update in order to avoid missing library errors.

### **PROGRAMMING LANGUAGE**
Arventa Connect iOS uses the latest Swift version, Swift 5, for development.

### **MINIMUM VERSION**
AtlasFX iOS requires devices with at least iOS 12.0
### **APPLICATION ID**
au.com.arventa.rc
### **DEBUGGING**
We use a few debugging tools to test Arventa Connect’s functionalities.
For the Native App, we use Xcode's debugging console to create breakpoints and test variables, API responses, and identify null objects which sometimes causes the crash.
To test the API before integrating for app usage, we use Postman (https://www.getpostman.com/). Postman is a very reliable REST API tool. We can test different HTTP Methods especially POST, PATCH, PUT, DELETE and GET. We can also add header variables to test SSO and token authentications.
We also use iOS Simulator in order to test the apps in different screen sizes and iOS Versions.

### **WEB API**
https://www.arventa.com.au/authservice
https://www.arventa.com.au/userservice
The authservice is used for authentication purposes and the userservice is used to retrieve and push data to the server. We are using Postman to test the web API endpoints in order to determine which endpoints are properly working and have bugs.

### **APPLICATION ARCHITECTURE**
The project uses an offline-first approach and does the syncing of local data with the server data on the background. This is to allow the continuous usage of the app while offline without interruptions.




### **THIRD PARTY LIBRARIES**
Most of the third party libraries are installed using CocoaPods. They can be added by searching library names found in https://cocoapods.org/, inserting them in the Podfile and running the pod install command in the Terminal.

#### **Important Libraries**
SQLCipher - an encrypted version of SQLite for the app’s DBMS. 
Alamofire - used to handle app communication with the Web API.
SwiftyJSON - used to handle JSON objects and have the fields be easily checked for nulls before converting to swift objects.
SwiftDate - used to handle Dates to have an ease of adding days and comparing dates.
ObjectMapper - used alongside SwiftyJSON in order to convert JSON objects to swift objects.
Reachability - used to check internet connection before loading the API and prevent users from further actions.

SAMKeychain - used to save the user’s device ID on the keychain to have a single unique ID even if the app is uninstalled and reinstalled.
Firebase/Analytics - a mobile SDK library for Google Analytics platform used to analyze usage data from users.
Firebase/Crashlytics - used to report crashes from Users that are not encountered during development and debugging.

#### **UI Libraries**
IBAnimatable - used to customize UI Views to match the designs more accurately.
MBProgressHUD - used to indicate that the items are loading and prevent user interaction until the items are loaded.
IQKeyboardManager - used to implement Keyboard avoiding when entering data into text-fields that are covered by the iOS On-screen Keyboard.
SDWebImage - used to set images on UIImageViews asynchronously using URLs.
SideMenu - used to implement the side menu view.
JVFloatLabeledTextField - used for the username & password fields.


### **ACTIVITIES AND CONTROLLERS**
#### **Core Classes**
ArventaInterface - used by view controllers to access data from the database. It is used to retrieve data and to save data.
ArventaWeb - used by ArventaSync class to communicate with the web API. It mostly contains functions that are related to the internet activities of the app like saving to the server or retrieving records from the server.
ArventaDB - used by ArventaInterface and ArventaSync classes to communicate with SQLite. It mostly contains functions that are related to the DBMS and contains queries.
ArventaSync - a singleton class which contains most of the core functions of the app’s synchronization functionality.  It contains functions to save and retrieve data from the web and updates the data in the database. This is the class where the NotificationCenter listeners are added to allow seamless synchronization with the server and local data.
AppDelegate - contains handlers for application states. It also handles deep linking to direct users to specific screens depending on the URL specified.
ArventaViewDelegate - most of the view controllers in the app conforms to this protocol and it contains global functions that are accessible throughout the development and avoid redundant functionalities.
HUDDelegate - view controllers that conforms to this protocol are able to show or hide HUDs if there are web API functions executed.
Models Swift Files - contains the model classes with their functions that returns different values and statements to be used as output for views.

#### **View Controllers**
MainNavigationController - the main navigation controller used to change view controllers accordingly. It is mostly accessed by the side menu view controller to change root view controllers based on the selected menu items. 
SideMenuViewController - contains functions that displays user’s available side menu items. It handles the selection of the menu items and also contains the log out button.
Authentications
SignInViewController - contains functionalities to allow users to log in on the app. It handles redirection to either the dashboard or mobile verification screen.
VerifyAccountViewController - contains functionalities to allow users to verify their accounts using one time codes sent on their respective mobile numbers.
Landing View Controllers
DashboardViewController - contains functionalities that displays useful information for the user. It also displays the greeting and user’s name on the dashboard page.
StorageListViewController - contains functionalities that displays the list of Storages saved by the user or retrieved from the API. This is where the user can choose many options with existing storages like going to products list, updating storage compliance, completing location audit and re-inventory.
StorageSearchViewController - similar to Storage List, but only displays a list of storage that matches the search text.
UpsertStorageViewController - contains controls that users can use to enter data for new storage or update existing ones. The storage can then be saved and uploaded to the API.
ScanQRViewController - contains functionalities that users can use to scan QR codes and be used when updating storage data and other data models.
ProductListViewController - contains functionalities that displays the list of products of specific storage. The user can choose to add new products through here, move products to different storage and archive products.
ProductSearchViewController - similar to product list, but only displays a list of products that matches the search text.
SelectStorageViewController - displays a list of storage where the user can pick to transfer products to.
SelectProductsViewController - displays a list of products that users can select to be transferred to another storage.
UpsertProductViewController - contains functionalities that users can use to enter data for new products or update existing ones. The product can then be saved and uploaded to the API.
ReinventoryStorageViewController - contains functionalities where the user can see specific storage in re-inventory and displays list of products.
