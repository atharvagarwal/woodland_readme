
# Woodland App

E-commerce app for  Woods , A Skating Monk & Woods Sports
## Setting Up The Project

1. The app is built using react-native with expo and in case you have never used expo and want to learn about setting it up from scratch you can follow https://docs.expo.dev/tutorial/create-your-first-app/ to setup your first app.

2. Incase you know about how expo works you can directly clone the app from github using the command **git clone url**

3. now **cd** into the directory , run **npm install** , **npx expo start** in order.
# Project Name

## Overview

This project is structured as a modern application with several key folders for organization, reusable components, and efficient management of app functionality.

# Project Name

## Overview

This project is structured as a modern expo application with usage of expo router containing several key folders for organization, reusable components, and efficient management of app functionality.

## Folder Structure

```bash
.
├── app/ (automatic routing is done)
│   ├── _layout.tsx           # Layout of the app
|   │  auth/                  # Initial entry point of the app in logged in state contains pages for (e.g., Explore, Cart) with a default _layout.tsx file
|   ├── _layout.tsx
|   ├── index.tsx
|   ├── Otp.tsx
|   ├── SignIn.tsx
|   |
|    tabs/                     # Initial entry point of the app in not logged in state &contains tabs for (signin , otp etc) with a default _layout.tsx file
|   ├── _layout.tsx
|   ├── Cart.tsx
|   ├── Categories.txt
|   ├── Explore.tsx
|   ├── home.tsx
|   ├── Orders.tsx
|   |        
│   ├── +native-intent.tsx
│   ├── +not-found.tsx
│   ├── Checkout.tsx
│   ├── OrderDetail.tsx
│   ├── ProductDetail.tsx  
│   ├── Success.tsx  
│
├── assets/
│   ├── images/               # Folder for app images
│   └── fonts/                # Folder for app fonts
│
components                     # Folder for several types of reusable components used within the app.
├── base
│   ├── /Button/Button.tsx
│   └── /Header/Header.tsx
├── cart
│   └── Card.tsx
├── checkout
│   ├── Address.tsx
│   ├── AddressForm.tsx
│   ├── Bill.tsx
│   ├── Discount.tsx
│   └── Donation.tsx
├── common
│   └── form
│       └── ControlledInput.tsx
├── orders
│   ├── OrderList.tsx
│   ├── OrderDetails.tsx
│   └── OrderHistory.tsx
├── products
│   ├── ProductList.tsx
│   ├── ProductDetails.tsx
│   └── ProductSearch.tsx
└── tests
|   |__ styledtext-test.js
└── utilities
|   |__ securityClient.ts
│
hooks\api
├── checkout
│   ├── query.tsx
│   └── types.ts
├── order
│   ├── query.tsx
│   └── types.tsx
├── product
│   ├── query.tsx
│   └── types.tsx
    └── index.tsx
├── reactquery.tsx
├── types.ts
│
├── store/
│   └── store.ts              # State management files based on Zustand
├── utils/
│   └── rules.ts              # Form validation rules and utility functions
│
├── config/
│   └── config.ts             # Configuration settings for environment variables, API keys, and other libraries for axios etc
```
## App Folder Breakdown

The app folder consists of the files & folders mentioned the folder structure above and now we are going to discuss about each of them in detail . Moreover , we use expo router for the routing purpose.

1.**layout.tsx**

This file sets up the global structure and services for an Expo app. This our app we initializ Sentry for error and performance tracking, including navigation tracking via ReactNativeTracing. Amplitude is set up for event analytics, and platform-specific logic is used to fetch referrer details on Android and request tracking permissions on iOS. The QueryClientProvider enables API request management using React Query, and the Stack component handles screen navigation. Sentry wraps the entire layout to monitor unhandled errors, ensuring a robust, tracked app experience across various functionalities.

2.**(auth.tsx)**
It is the inital entry point of the application and consists of the following files->

**_layout.tsx** - The Layout component provides a safe and structured container for rendering screens in the app. It uses SafeAreaView from react-native-safe-area-context to ensure content avoids system UI elements like the status bar or notch. The Slot component acts as a placeholder where child routes or screens will be rendered dynamically. The styles.top applies a background color from the Colors.light.background constant and ensures that the view takes up the full height of the screen using flex: 1. This setup creates a flexible and visually consistent layout for the app's navigation structure.

**index.tsx** - This contains the GetStarted component displays a full-screen image carousel, using an array of image paths that change every 3 seconds via the useEffect hook. It checks if the user is logged in using isLoggedIn(), and if so, redirects them to the home screen. Otherwise, the user can manually navigate to the sign-in page by pressing the "Next" button, rendered by the CustomButton component. The images are displayed within a container that takes up the full width of the screen, with the button positioned near the bottom for navigation purposes. The layout is styled using StyleSheet for flexibility and responsiveness.

**Signin.tsx** - This code creates a simple login/registration screen. Users enter their mobile number, and upon pressing "Send OTP", an OTP is sent to the provided number. If the number is valid (and matches a specific number for testing), the user is immediately redirected to the OTP screen.

**Key components and logic:**

ControlledInput: A custom input component that handles user input.

onSubmit: This function is called when the "Send OTP" button is pressed. It validates the mobile number and sends an OTP if valid.

Validations: The code likely includes basic validations like checking if the number is 10 digits long and numeric.

API Integration: The code probably makes an API call to send the OTP to the user's mobile.

Conditional Navigation: If the mobile number matches a specific number (e.g., for testing), the user is immediately redirected to the OTP screen.

Overall, this code provides a basic framework for mobile number authentication in a React Native app.

**Otp.tsx** - The Otp component is a screen for verifying a user's login via a 6-digit OTP (One-Time Password). It uses React Native's CodeField for OTP input and includes features for OTP submission, login verification, and resending the code.

**Key components and logic:**

OTP Input Handling: It uses CodeField with useBlurOnFulfill and useClearByFocusCell to handle OTP input and focus behavior. The entered OTP is stored in the value state.

Login Verification: The handleSubmit function submits the entered OTP. If the OTP is 000000, it simulates a successful login by setting a mock authentication token and navigating the user to the home screen. Otherwise, it calls the mutate function from useVerifyLogin() to validate the OTP.

API Call: It uses the mutate method from useVerifyLogin() to call the login API, which either sets the authentication token and user ID or displays an error alert if the OTP verification fails.

Loading State: If the verification is in progress (isPending), it shows an ActivityIndicator.

Resend OTP: The user can navigate back to the previous screen to resend the OTP by clicking "Resend Code."
UI Layout: The component includes a title, description, OTP input field, and a button to verify the OTP, all styled with the StyleSheet.

Overall, this component manages OTP-based login verification with responsive UI feedback and handles both success and error scenarios.

3.**(tabs)**

**_layout.tsx**
This code creates a tab-based navigation layout using expo-router in a React Native app. It defines four screens (Home, Explore, Cart, Orders), each represented by a tab with custom icons from FontAwesome, AntDesign, and SimpleLineIcons. The screenOptions function sets dynamic properties for all tabs, such as the active tab color using Colors.common.primaryButton and showing a custom Header component that changes its title based on the current route. Tabs like Explore, Cart, and Orders use unmountOnBlur to unload their content when not in focus, optimizing performance.

**Cart.tsx**
The Cart component in React Native displays products added to the cart using useCustomStore to fetch the cartProduct list.

**Key Features:**

Empty Cart: If the cart is empty, it shows a "Your cart is empty" message with a "Shop Now" button that navigates to the home screen.

Cart Items: If items are present, it maps over the cartProduct array and renders each item as a CartCard with product details (image, title, price, etc.).

Checkout Button: At the bottom, a "Checkout" button navigates the user to the checkout page.

The component uses a ScrollView for scrolling through items and is styled for proper alignment and layout.

**Explore.tsx**

The Explore component is a product listing page with filtering options, infinite scrolling, and data fetching in a React Native app. It consists of the following key features:

**Key Features:**

State Management: The component uses a state variable (openFilter) to control the visibility of the filter modal. It also retrieves and manages filters via a global store (useCustomStore).

Data Fetching: It uses a custom hook (useGetInfiniteProducts) to fetch paginated product data, combining both URL search parameters and selected filter options.

Loading and Error Handling: While the data is loading, an ActivityIndicator is shown. If no products are found or an error occurs, it displays an alert message.

Product Listing: The FlatList component renders the product cards in a grid format, allowing for infinite scrolling. When the user reaches the end of the list, it fetches more products unless there are no more results.

Filter Modal: A floating filter icon is available at the bottom right, allowing users to open a filter modal and apply filters to the product list.

**Optimization:**

useCallback is used in combination with useFocusEffect to reset filters and close the filter modal only when the component gains or loses focus, preventing unnecessary re-renders.

**Home.tsx**

The Home page is a main screen in a React Native app that features:

Data Fetching: It fetches product data for best sellers, woods collection, and a special brand collection using custom hooks.

Loading State: Shows an ActivityIndicator while data is loading.
UI Layout:

Category List: Displays a list of product categories.

Discount Banner: Clickable image linking to an "Explore" page with offers.

Product Sections: Displays horizontal FlatList components for best sellers, woods, and Askatingmonk products, each with a header and a "view all" option.

Brand Banners: Clickable images linking to detailed views for specific brands.

The component uses ScrollView to layout the sections vertically and TouchableOpacity for navigation.

**Orders.tsx**

The Orders component is designed to display a user's order history.

Authentication Check: On mount, it checks if the user is logged in using the isLoggedIn function. If the user is not authenticated, it displays an alert and redirects them to the home screen.

Data Fetching: It uses the useGetUserOrders hook to fetch the user's orders. During this process:

If data is loading, an ActivityIndicator is shown.
If there's an error and no data is fetched, an error alert is displayed.
Rendering: Once data is loaded:

The SafeAreaView ensures content is displayed within the device's safe area.
The FlatList component is used to render a list of orders. Each order includes:
Basic order details (e.g., order ID, creation date).
Sub-orders displayed using the OrderCard component, which includes details like image, title, quantity, size, and status.
Styling: The component is styled for layout and visual appeal, ensuring consistent spacing and borders between order items.

This approach ensures a smooth user experience with proper error handling and data display.

4.**+native-intent.tsx**
The redirectSystemPath function is designed to convert a specific URL path into a new format for redirection. Here’s a breakdown:


In the context of React Native, particularly with file naming conventions, the + symbol before a file name, like +native-intent.tsx, typically indicates that the file is a dynamic route or special file used for routing or navigation purposes. This convention is often used in projects that employ routing libraries or frameworks that support dynamic or parameterized routing.

Parameters:

In the context of React Native, "intents" are a concept borrowed from native mobile development, particularly in Android. They represent a messaging system used to request actions or interact with other components or applications.

path (string): The URL path to be transformed.
initial (boolean): A flag indicating whether the function should perform a transformation or not.
Functionality:

Logging: It logs the path and initial parameters to the console for debugging purposes.
Condition: If initial is true, it proceeds with the path transformation.
Path Matching: Uses a regular expression to check if the path matches the pattern /product-detail/{slug}, where {slug} is a dynamic segment.
If a match is found, it extracts the {slug} from the URL.
Returns a new URL string in the format /ProductDetail?slug={slug}.
Usage:

This function is useful for redirecting or converting paths in a routing system, specifically from a path structure like /product-detail/{slug} to a query parameter format like /ProductDetail?slug={slug}.
Overall, it simplifies the process of handling and transforming specific URL patterns for redirection purposes.

5.**+not-found.tsx**

The NotFoundScreen component displays an alert with the message "No results found! Returning to home page" and then redirects the user to the home page using the Redirect component from expo-router. This is typically used to handle scenarios where a requested resource is not found, guiding users back to the main part of the app.

6.**Checkout.tsx**

The Checkout component in React Native manages the checkout process for an e-commerce app:

State Management: Handles states for promo codes, total amount, shipping charges, and payment methods (COD or prepaid).

Form Handling: Uses react-hook-form for validating user details and promo code input.

Pincode Validation: Updates shipping and payment options based on the entered pincode.

Promo Code: Allows users to apply/remove promo codes and adjusts discounts accordingly.

Order Creation: Supports prepaid and COD payments, integrates with Razorpay, and navigates to a success page.

UI Components: Displays order summary, product list, and address fields, with donation options and loading indicators.

Error Handling: Alerts users for errors like invalid pincode or promo code issues.

Analytics: Tracks checkout failures with Amplitude.
The component integrates form handling, payment processing, and UI management to ensure a seamless checkout experience.

7.**OrderDetail.tsx**

The OrderDetail component in React Native:

Data Fetching: Uses useGetOrderDetail to fetch order details based on orderid.
Loading & Errors: Shows a spinner during loading and an alert if there's an error.
UI Components:
Order Summary: Displays items with OrderDetailCard, showing details like image, name, price, and quantity.
Billing Information: Uses Bill to show subtotal, donation, discount, delivery charges, and total amount.
Shipping Address: Shows contact info and shipping address.
Navigation: Includes a "Go back" button to return to the previous screen with router.back().
Layout & Styling: Uses SafeAreaView and StyleSheet for responsive design and consistent styling.

8.**ProductDetail.tsx**
The compoenent Displays detailed product information and handles user interactions.

**Key Features:**

Product Details: Shows images, title, price, and description of the product.
Size Selection: Users can select product sizes.

Add to Cart: Adds the selected product size to the shopping cart.
Pincode Check: Validates delivery availability based on user-entered pincode.

Size Chart: Provides a size chart for reference.
UI Handling:

Loading: Displays a spinner while fetching data.
Error Handling: Shows error messages if something goes wrong.
Tracking:

Add to Cart: Sends an event to Amplitude when a product is added to the cart.

Product View: Sends an event to Amplitude when a product is viewed.
Layout:

Header: Displays a header at the top.

Product Carousel: Shows a carousel of product images.
Size Options: Lists available sizes and indicates if they are in stock.

Action Buttons: Includes "Add to Cart" or "Go to Cart" buttons based on cart status.

Pincode Checker: Allows users to enter a pincode for delivery validation.

9.**Success.tsx**

The Success component displays a confirmation screen after an order has been placed. It handles data fetching, revenue tracking, and UI rendering.

**Key Features**

Data Fetching: Uses useLocalSearchParams to extract the orderId from the URL parameters.

Fetches order details using useGetOrderDetail.
Revenue Tracking:

Defines a function handelRevenueEvent to create and log revenue events with Amplitude.

Tracks each sub-order's revenue details like product ID, price, quantity, and promo code.

Loading and Error Handling: Shows a loading indicator (ActivityIndicator) while fetching data.

Displays an error alert if data fetching fails and navigates to the home screen.

UI Elements: Displays a success image.
Shows a confirmation message and the order ID.
Includes a button that navigates to the orders screen.

## Components 

1.**/Base/Button**
The CustomButton component in React Native renders a button with three style options: 'primary', 'secondary', and 'tertiary'. The button's appearance changes based on the type prop:
Primary: A solid button with a background color.
Secondary: A bordered button with no background.
Tertiary: A button with no specific style.
It also displays a customizable title and triggers an onPress function when clicked. The styles and layout are dynamically adjusted based on the type prop, ensuring flexibility in design.

2.**/Base/Header**
This Header component in React Native displays a customizable header with search and drawer functionalities:
Props: It takes a title and an optional onExplore boolean.
State Management: It manages states for search visibility (searchBar), search input (searchText), and drawer visibility (drawerPress).
Search Bar: When active, it displays a TextInput for search and routes to the Explore page based on input.
Drawer: Tapping the drawer icon shows a modal (DrawerModal) with options for logging out and deleting the account.
Cart & Search Icons: The header has icons to toggle the search bar and navigate to the Cart screen.
This component is well-structured for dynamic title display and navigation functionality.

3.**Cart**
This CartCard component in React Native represents an item in a shopping cart. Here's a breakdown of its features:
Props:
id, imageUrl, title, price, color, size, quantity: The card displays an image, item details (color, size, price), and quantity.
pickerEnabled: A boolean that controls whether the quantity can be updated via a dropdown.
Main Features:
Image Display: Shows the product image using Expo's Image component with a loader (woodland-loader.gif).
Details: Renders the item's title, price, color, size, and quantity.
Quantity Picker: If pickerEnabled is true, users can change the quantity via a dropdown. The dropdown toggles open/close states.
Remove Functionality: Users can remove the item from the cart.
Interactions: The quantity picker allows users to select between 1, 2, or 3, and the removeFromCart function deletes the item.
State:
Manages the dropdown state (open) to toggle between showing or hiding the quantity picker.
This component is a flexible and reusable card for displaying cart items with the ability to modify the quantity and remove items from the cart.

4.**Checkout**

**Address.tsx**
The AddressCard component in React Native displays a user's address with an option to confirm delivery.

Props:

address: A string containing the address.
Features:

Address Display: Shows a "Home" label and the provided address.
Delivery Button: A "Deliver to this address" button logs a message when pressed.
Styles:

Container: Light background with rounded corners, shadows, and elevation, taking up 95% of the screen width.
Header: Displays the "Home" label and address with padding.
Button: Green with bold white text for the delivery option.
This reusable component suits checkout processes or address books.

**AddressForm.tsx**

The AddressForm component is a React Native form designed for collecting address details. It uses react-hook-form to handle form state, validation, and submission.

Key Features:
Form Fields: Includes fields for houseNumber, city, pin, state, and landmark. Each field is managed with ControlledInput, a custom component that integrates with react-hook-form for controlled input management.
Validation: Essential fields (houseNumber, city, pin, state) have validation rules to ensure they are filled out correctly, with custom error messages for each.
Reset Button: Positioned at the top-right, this button clears the form data when pressed.
Layout: Utilizes flexbox for arranging the inputs, with responsive styling that adapts to screen width. The form is padded and has a light background with a border at the top for visual separation.
This component is useful for adding new addresses in an application, ensuring users provide all necessary information with built-in validation and a reset option.

**Bill.tsx**

The Bill component displays a detailed financial summary with the following features:

Props: Accepts subtotal, donation, discount, deliveryCharges, and total.
Layout: Each financial item (e.g., subtotal, donation, discount) is shown in its own row with labels and formatted values.
Total: The final amount is highlighted at the bottom in a bold and larger font.
Styling: Uses a light background with rounded corners and a border for a card-like appearance. Text is formatted for clarity and readability.
Design: Ensures a clear, organized view of charges and totals for easy user review.

**Donation.tsx**

The Donation component allows users to opt-in for updates and add a donation to their transaction. Here’s a breakdown:

Props: Receives an onSelect function to notify changes.
State: Manages two boolean states:
receiveUpdates: Tracks user preference for receiving updates.
addDonation: Manages if a ₹30 donation should be added to the transaction.
Checkboxes:
The first checkbox lets users opt-in for updates on products and promotions.
The second checkbox allows users to add a ₹30 donation, triggering onSelect when changed.
Styles: The component uses a light background and aligns checkboxes with labels for a clear and user-friendly layout.

5.**ControlledInput**
The ControlledInput component integrates with React Hook Form to provide a versatile input field with additional functionalities:

Props:
Inherits all standard TextInput props.
Custom props include icon (for visual icons), name (form field name), rules (validation rules), control (hook form control object), containerStyle, rootContainerStyle, inputContainerStyle, isPassword (for password fields), countryCode (for handling country codes), and onCountryChange (callback for country changes).

State Management:

Maintains a secureText state to toggle password visibility.
Controller Integration:

Utilizes React Hook Form's Controller to bind form state and handle validation seamlessly. The Controller component manages field value and error state, ensuring smooth integration with the form.

Rendering:

Renders a TextInput with optional password visibility toggle using an Ionicons icon. Displays error messages if validation fails.
Applies custom styles provided through props to adjust appearance and layout.
The component is designed to be flexible, supporting various input types and customizations while handling form validation and state management efficiently.

6.**ProductDetail**

**PincodeChecker.tsx**
The PincodeChecker component is used for handling pincode input with validation.

Key Features:
Props:

onPress: Callback triggered when the "Check" button is pressed.
control: React Hook Form’s Control object for managing form state and validation.
name: Name of the form field for React Hook Form.
maxLength (optional): Limits the pincode input length.
Components:

ControlledInput: Custom input field integrated with React Hook Form, styled for pincode entry.
TouchableOpacity: Button labeled "Check", triggering the onPress function.
Styles:

pincodeContainer: Flex container for layout.
pincodeButtonContainer: Contains the ControlledInput.
checkButton: Styled button for submission.
Usage:
Ideal for scenarios needing pincode input, such as code verification or delivery checks.

**ProductCarousel.tsx**
The ProductCarousel component displays a horizontal image carousel with pagination indicators.

Key Features:
Props:

images: Array of image URLs for the carousel.
Components:

Img: Renders each image with a loading indicator.
FlatList: Displays images horizontally, with paging enabled.
ActivityIndicator: Shows a loading spinner while images load.
Functionality:

Image Handling: Images are displayed in a scrollable carousel. An ActivityIndicator is shown while images load.
Pagination: Dots below the carousel indicate the current image. The active dot’s opacity changes based on the currently visible image.
Styles:

dotContainer: Container for pagination dots.
dot: Style for pagination dots with variable opacity.

Usage:
Ideal for displaying multiple images in a scrollable format with visual indicators for the current image.

7.**Orders**

**OrderCart.tsx**
The OrderCard component displays an order's details with options to view or cancel the order.

Key Features:
Props:

imageUrl: Image source for the product.
title: Product title.
subtitle: Quantity of the product.
size: Size of the product.
orderId, subOrderId: Identifiers for the order.
cancellable: Determines if the order can be canceled.
status: Current status of the order.
Components:

Image: Displays product image with a placeholder and caching.
ActivityIndicator: Shows a spinner while canceling the order.
TouchableOpacity: Buttons for viewing order details and canceling the order.
Functionality:

View Details: Navigates to order detail page.
Cancel Order: Prompts confirmation and cancels the order if confirmed. Updates the order list and handles errors.
Styles:

Container: Card with shadow and padding for the order.
Row: Layout for image and details.
Button: Styled for "View Details" and "Cancel" actions.
Usage:
This component is used to present individual order details with actions to view more information or cancel the order, depending on its status.

**OrderDetailCard.tsx**

The OrderDetailCard component displays detailed information about an individual order item.

Key Features:
Props:

url: Image URL of the product.
title: Product title.
color: Color of the product.
quantity: Quantity ordered.
size: Size of the product.
price: Original price of the product.
finalPrice: Discounted or final price.
subOrderId: Unique identifier for the sub-order.
Components:

Image: Displays the product image.
Text: Shows product details like title, color, size, quantity, and price.
Functionality:

Price Display: Shows the original price with a line-through if it differs from the final price. Displays the final price prominently.
Styles:

Root: Card layout with border, padding, and spacing.
Image Container: Section for product image.
Product Detail Container: Section for product details.
Price Details Container: Section for displaying prices.
Usage:
This component is used to present detailed information about an item in an order, including its image, specifications, and pricing, with clear differentiation between original and final prices.

8.**Common**

**Accordion.tsx**
in a bit short
ChatGPT said:
ChatGPT
The Accordian component provides a collapsible section for displaying and hiding content.

Props:

title: Header text.
onLinkPress: Optional callback for link press.
href: Optional navigation link.
children: Content to show when expanded.
dropdown: Controls whether the component has a dropdown arrow (default is true).
subDrawer: Adjusts styling for sub-items.
Features:

Toggle Function: Clicking the header toggles the visibility of the content.
Icon: An arrow icon indicates whether the section is expanded or collapsed.
Styles:

link and subLink: Style for text and layout based on whether it's a main item or a sub-item.
text and subText: Font styles for the header text.
This component is used for creating expandable sections in a UI, ideal for menus or settings.

**CategoryButton.tsx**

The CategoryButton component is a customizable button for React Native.

Props:

text: Button label.
onPress: Function to call when the button is pressed.
backgroundColor: Button's background color.
textColor: Text color.
id: Unique identifier for the button.
Features:

Style: The button uses Pressable for press handling and supports custom colors for both background and text.
Layout: The button is styled with rounded corners and center-aligned text.
Usage:

The CategoryButton component can be used for various interactive elements where customization of colors and text is needed, such as category filters or action buttons.

**CategoryList.tsx**

The CategoryList component is a horizontal scrollable list of category buttons.

Features:

Data Handling: It uses an array of category names (data) to render buttons.
State Management: Keeps track of the selected category with selectedId and updates it on button press.
Navigation: Uses useRouter from expo-router to navigate to a category-specific page when a button is pressed.
Components:

ScrollView: Allows horizontal scrolling of the category buttons. Styled to ensure proper height and background color.
CategoryButton: Custom button component that changes appearance based on whether it is selected or not.
Usage:

Ideal for displaying a list of categories where users can select one to view related content. The selected category is highlighted, and pressing a button navigates to a category-specific page.

**drawerModal.tsx**

The DrawerModal component creates a modal drawer for navigation and settings.

Features:

Visibility: Controlled via visible prop.
Content: Displays a close button, logo, and a list of navigational links organized into expandable accordions.
Accordions: Show/hide sub-items for categories like Footwear, Topwear, and Bottomwear. Additional settings option for iOS/macOS users.
Navigation: Uses Link for routing to various sections.
Platform Handling: Adjusts for Android status bar and applies specific styling based on the platform.
Usage: Ideal for providing a detailed navigation menu and settings options within an app, with support for hierarchical categories and conditional content based on the platform.

**FilterComponent.tsx**

The FilterComponent is a React Native component designed to display and manage a set of filter options. Here's a concise overview:

Purpose: Allows users to filter items based on categories like gender, size, color, sort, and price.

Props:

onClose: Callback function to handle closing the filter modal.
State Management:

Uses useCustomStore to manage the selected category and options, and to reset filters.
Components:

Filter Categories: Displays clickable categories (e.g., gender, size).
Options: Displays options for the selected category, allowing users to select or deselect filters.
Buttons: "Clear All" button to reset filters, "Close" and "Apply" buttons to close the filter modal.
Styles:

Uses StyleSheet for layout and styling, with a focus on usability and visual distinction between selected and unselected options.
Functions:

handleCategoryClick: Sets the current filter category.
handleOptionClick: Updates selected options based on user interaction.
handleCancelFilters: Resets all filters.
This component is designed to be flexible and reusable, integrating with a state management system to update and apply filters dynamically.

**ProductListingCard.tsx**
Purpose: Displays a product card with an image, title, pricing, and color options.

Props:

title: Product title.
price: Original price.
offerPrice: Discounted price.
productImageUrl: Main image URL.
productMeta: Color options with URLs.
Functionality:

Shows main product image and discount badge if applicable.
Displays both original and discounted prices.
Renders clickable color thumbnails that update the main image and navigate to product details.
Navigation: Uses expo-router to change route based on selected color's slug.

**Size.tsx**
Purpose: Displays a size option with customizable styling based on availability and state.

Props:

size: Size text to display.
soldOut: Optional; if true, indicates the size is unavailable.
color: Background color of the size option.
inCart: Optional; if true, the size is in the cart.
Functionality:

Displays a circular box with the size text.
If soldOut, applies a gray background and ensures text color is white.
If inCart, ensures text color is white.
If no soldOut or inCart, text color is black and background is set by color.
Styling:

root: Basic style for available sizes.
soldRoot: Style for sizes marked as sold out.

**SizeChart.tsx**
Purpose: Displays a modal with size charts for shoes or garments based on the type prop.

Props:

visible: Controls the visibility of the modal.
type: Determines the chart type, either "SHOES" or "GARMENTS".
onCrossPress: Optional; function called when the close button is pressed.
Functionality:

Shows size charts for different categories (men's and women's shoes, and men's and women's garments).
Each chart includes size measurements in various units (UK, EURO, CM for shoes; chest measurements for garments).
Alternates row colors for better readability.
Styling:

Uses SafeAreaView for proper layout.
Includes a close button using Entypo and adjusts text and background colors based on the chart type.
Usage:

For garments: Displays charts for men's and women's tops and bottoms.
For shoes: Displays charts for men's and women's shoes.
