
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


### **_layout.tsx**

The `_layout.tsx` component is responsible for providing a structured container for rendering screens throughout the app.

- **SafeAreaView:**
  - Ensures content avoids system UI elements like the status bar or notch, maintaining a clean and accessible layout.
- **Slot Component:**
  - Serves as a placeholder for dynamically rendering child routes or screens, allowing for flexible navigation and screen transitions.
- **Styles:**
  - Uses `styles.top` to apply a background color sourced from `Colors.light.background`.
  - Ensures the view occupies the full height of the screen using `flex: 1`, creating a consistent layout across different screens.

This setup ensures a flexible, visually consistent layout for the app’s navigation structure.

### **(auth) folder breakdown**

### **index.tsx**

The `index.tsx` component displays a full-screen image carousel with the following features:

- **Image Carousel:**
  - Cycles through an array of image paths every 3 seconds, providing users with a dynamic visual experience.
  - Implemented using the `useEffect` hook to handle the automatic image rotation.
- **User Authentication Check:**
  - Uses the `isLoggedIn()` function to check user authentication status.
  - Redirects logged-in users to the home screen, bypassing the introductory screens.
- **Navigation:**
  - Provides a "Next" button, rendered by the `CustomButton` component, allowing users to proceed to the sign-in page.
- **Layout:**
  - Styled using `StyleSheet` to ensure flexibility and responsiveness, adapting to various screen sizes.

### **Signin.tsx**

The `Signin.tsx` component serves as the login/registration screen with the following key features:

- **Mobile Number Input:**
  - Allows users to enter their mobile number to receive an OTP for authentication.
- **OTP Request:**
  - Sends an OTP to the provided number when the "Send OTP" button is pressed.
- **Validations:**
  - Includes basic validations to ensure the mobile number length and format are correct.
- **API Integration:**
  - Makes an API call to send the OTP, ensuring backend communication for authentication.
- **Conditional Navigation:**
  - Redirects users to the OTP screen immediately if the entered number matches a specific test value.

This component establishes the initial step for mobile number authentication in the app.

### **Otp.tsx**

The `Otp.tsx` component manages OTP-based login verification with these key features:

- **OTP Input Handling:**
  - Utilizes `CodeField` with `useBlurOnFulfill` and `useClearByFocusCell` for handling OTP input and managing focus behavior.
- **Login Verification:**
  - Submits the OTP via `handleSubmit`. If the OTP is `000000`, it simulates a successful login by setting a mock authentication token and navigating to the home screen.
  - Otherwise, it uses `mutate` from `useVerifyLogin()` to validate the OTP with the backend API.
- **API Call:**
  - Interacts with the login API using `mutate` from `useVerifyLogin()`, handling both success and error scenarios.
- **Loading State:**
  - Displays an `ActivityIndicator` while verification is in progress to provide feedback to the user.
- **Resend OTP:**
  - Offers an option to resend the OTP by navigating back to the previous screen, enhancing user experience.
- **UI Layout:**
  - Includes a title, description, OTP input field, and a verification button, all styled with `StyleSheet` for a cohesive design.

This component efficiently manages OTP-based login verification and provides responsive UI feedback throughout the process.




### **(tabs) folder breakdown**
### **Cart**
The **Cart** component includes functionalities and UI elements related to cart management:

- **Empty Cart**: 
  - Displays a message "Your cart is empty" with a "Shop Now" button that navigates to the home screen when the cart is empty.

- **Cart Items**:
  - Maps over the `cartProduct` array and renders each item as a `CartCard` with product details such as image, title, and price if items are present.

- **Checkout Button**:
  - Includes a "Checkout" button at the bottom that navigates the user to the checkout page.

- **ScrollView**:
  - Uses `ScrollView` for scrolling through cart items, styled for proper alignment and layout.

### **Explore.tsx**
The `Explore` component is a product listing page with filtering options and infinite scrolling. Key features include:

- **State Management**:
  - Uses a state variable `openFilter` to control the visibility of the filter modal.
  - Retrieves and manages filters via a global store (`useCustomStore`).

- **Data Fetching**:
  - Utilizes a custom hook (`useGetInfiniteProducts`) to fetch paginated product data, combining URL search parameters and selected filter options.

- **Loading and Error Handling**:
  - Displays an `ActivityIndicator` while data is loading.
  - Shows an alert message if no products are found or if an error occurs.

- **Product Listing**:
  - Uses `FlatList` to render product cards in a grid format with infinite scrolling.
  - Fetches more products when the user reaches the end of the list, unless there are no more results.

- **Filter Modal**:
  - Features a floating filter icon at the bottom right to open the filter modal and apply filters to the product list.

- **Optimization**:
  - `useCallback` and `useFocusEffect` are used to reset filters and close the filter modal only when the component gains or loses focus, preventing unnecessary re-renders.

### **Home.tsx**
The `Home` component serves as the main screen in the React Native app. Key features include:

- **Data Fetching**:
  - Fetches product data for best sellers, woods collection, and a special brand collection using custom hooks.

- **Loading State**:
  - Shows an `ActivityIndicator` while data is loading.

- **UI Layout**:
  - **Category List**: Displays a list of product categories.
  - **Discount Banner**: Clickable image linking to an "Explore" page with offers.
  - **Product Sections**: Features horizontal `FlatList` components for best sellers, woods, and Askatingmonk products, each with a header and a "view all" option.
  - **Brand Banners**: Clickable images linking to detailed views for specific brands.

- **ScrollView and TouchableOpacity**:
  - Uses `ScrollView` to layout sections vertically and `TouchableOpacity` for navigation.


### **Orders.tsx**

The `Orders` component displays a list of user orders and manages user authentication and loading states.

**Functionality:**

- **Authentication Check:**
  - Uses the `isLoggedIn` function to verify if the user is logged in.
  - If the user is not logged in, an alert is shown, and the user is redirected to the home screen using `router.navigate('/home')`.

- **Data Fetching:**
  - Retrieves user orders using the `useGetUserOrders` custom hook.
  - Displays an `ActivityIndicator` while data is loading.

- **Error Handling:**
  - If there is an error and no data is fetched, an alert is shown with the message "Orders not found! Please try again later."

- **UI Components:**
  - **Order List:**
    - Uses `FlatList` to render a list of orders.
    - Each order item displays order details and includes a list of sub-orders.
    - Each sub-order is rendered using the `OrderCard` component, which displays product details such as image, title, quantity, size, and status.

- **Styles:**
  - **`root`**: Sets the background color for the entire view.
  - **`orderInfoContainer`**: Styles the container for order information, including alignment and margins.
  - **`orderContainer`**: Styles the container for individual orders, including padding, border, and margins.

### **+native-intent.tsx**

In the context of React Native, the `+native-intent.tsx` file is used for handling dynamic routes or special navigation logic. The `+` symbol indicates that this file might be involved in routing or parameterized navigation.

**Functionality:**

- **Parameters:**
  - **`path` (string):** The URL path to be transformed.
  - **`initial` (boolean):** A flag indicating whether the function should perform a transformation or not.

- **Functionality:**
  - **Logging:** Logs the path and initial parameters to the console for debugging purposes.
  - **Condition:** If `initial` is true, it proceeds with the path transformation.
  - **Path Matching:** Uses a regular expression to check if the path matches the pattern `/product-detail/{slug}`, where `{slug}` is a dynamic segment.
    - If a match is found, it extracts the `{slug}` from the URL.
    - Returns a new URL string in the format `/ProductDetail?slug={slug}`.

**Usage:**

This function is useful for redirecting or converting paths in a routing system, specifically from a path structure like `/product-detail/{slug}` to a query parameter format like `/ProductDetail?slug={slug}`. It simplifies the process of handling and transforming specific URL patterns for redirection purposes.

---

### **+not-found.tsx**

The `+not-found.tsx` component is used to handle scenarios where a requested resource is not found. It provides a fallback mechanism to guide users back to the main part of the app.

**Functionality:**

- **Alert:** Displays an alert with the message "No results found! Returning to home page" when a resource is not found.
- **Redirection:** Uses the `Redirect` component from `expo-router` to navigate the user back to the home page.

**Usage:**

This component is typically used in routing systems to handle 404 errors or cases where a requested resource is unavailable, ensuring that users are redirected to the main page of the app.

### **Checkout.tsx**

The `Checkout.tsx` component manages the checkout process for an e-commerce app in React Native. It ensures a smooth user experience by handling various aspects of the checkout flow.

**Key Features:**

- **State Management:**
  - **Promo Codes:** Manages states for applying and removing promo codes.
  - **Total Amount:** Tracks the total amount due, including discounts and additional charges.
  - **Shipping Charges:** Updates shipping costs based on user input.
  - **Payment Methods:** Handles payment method selection, including Cash on Delivery (COD) and prepaid options.

- **Form Handling:**
  - Utilizes `react-hook-form` to validate user details and promo code inputs, ensuring accurate data collection.

- **Pincode Validation:**
  - Updates shipping and payment options based on the pincode entered by the user, verifying delivery availability.

- **Promo Code Management:**
  - Allows users to apply or remove promo codes, adjusting discounts and recalculating the total amount accordingly.

- **Order Creation:**
  - Supports both prepaid and COD payments.
  - Integrates with Razorpay for payment processing.
  - Navigates to a success page upon successful order completion.

- **UI Components:**
  - **Order Summary:** Displays a summary of the order, including items and their details.
  - **Product List:** Shows a list of products included in the order.
  - **Address Fields:** Presents user address and contact information.
  - **Donation Options:** Provides an option to add donations to the order.
  - **Loading Indicators:** Displays loading spinners during data processing.

- **Error Handling:**
  - Alerts users if there are issues such as invalid pincode or promo code problems, ensuring a smooth checkout experience.

- **Analytics:**
  - Tracks checkout failures and user interactions with Amplitude to gather insights and improve the checkout process.

**Overall,** `Checkout.tsx` integrates form handling, payment processing, and comprehensive UI management to create a user-friendly and efficient checkout experience.


### **OrderDetail.tsx**

The `OrderDetail.tsx` component displays detailed information about an order, providing users with an overview of their order's status and contents.

**Key Features:**

- **Data Fetching:**
  - Uses the `useGetOrderDetail` hook to fetch details of an order based on the provided `orderId`.

- **Loading & Errors:**
  - Displays a spinner (ActivityIndicator) while the order details are being fetched.
  - Shows an alert if there is an error in fetching order details.

- **UI Components:**
  - **Order Summary:** 
    - Utilizes `OrderDetailCard` to show each item's details, including image, name, price, and quantity.
  - **Billing Information:** 
    - Uses the `Bill` component to display the subtotal, donation amount, discount, delivery charges, and total amount.
  - **Shipping Address:**
    - Displays the user's contact information and shipping address.

- **Navigation:**
  - Includes a "Go back" button that uses `router.back()` to return to the previous screen.

- **Layout & Styling:**
  - Employs `SafeAreaView` and `StyleSheet` for responsive design and consistent styling across different devices.

### **ProductDetail.tsx**

The `ProductDetail.tsx` component provides a detailed view of a product and allows users to interact with it.

**Key Features:**

- **Product Details:**
  - Displays product information including images, title, price, and description.

- **Size Selection:**
  - Allows users to select from available product sizes.

- **Add to Cart:**
  - Adds the selected product size to the shopping cart.

- **Pincode Check:**
  - Validates the delivery availability based on the pincode entered by the user.

- **Size Chart:**
  - Provides a size chart to help users select the appropriate size.

**UI Handling:**

- **Loading:**
  - Shows a spinner (ActivityIndicator) while the product details are being fetched.

- **Error Handling:**
  - Displays error messages if there is an issue fetching product details or during other interactions.

**Tracking:**

- **Add to Cart:**
  - Sends an event to Amplitude when a product is added to the cart.

- **Product View:**
  - Sends an event to Amplitude when a product is viewed.

**Layout:**

- **Header:**
  - Displays a header at the top of the screen.

- **Product Carousel:**
  - Shows a carousel of product images for better visual presentation.

- **Size Options:**
  - Lists available sizes and indicates which sizes are in stock.

- **Action Buttons:**
  - Includes buttons such as "Add to Cart" or "Go to Cart" depending on the cart status.

- **Pincode Checker:**
  - Allows users to enter a pincode to check delivery availability.



### **Success.tsx**

The `Success.tsx` component provides a confirmation screen for users after they have successfully placed an order. It manages data fetching, revenue tracking, and renders the appropriate UI elements.

**Key Features:**

- **Data Fetching:**
  - **Order ID Extraction:**
    - Uses the `useLocalSearchParams` hook to extract the `orderId` from the URL parameters.
  - **Order Details:**
    - Fetches order details using the `useGetOrderDetail` hook based on the extracted `orderId`.

- **Revenue Tracking:**
  - **Revenue Event Handling:**
    - Defines the `handelRevenueEvent` function to create and log revenue events with Amplitude.
    - Tracks revenue details for each sub-order, including product ID, price, quantity, and any applicable promo codes.

- **Loading and Error Handling:**
  - **Loading Indicator:**
    - Displays a loading indicator (ActivityIndicator) while the order details are being fetched.
  - **Error Handling:**
    - Shows an error alert if there is a failure in fetching order details.
    - Navigates to the home screen if data fetching fails.

- **UI Elements:**
  - **Success Image:**
    - Displays a success image indicating the successful placement of the order.
  - **Confirmation Message:**
    - Shows a confirmation message along with the `orderId` to inform the user that their order has been placed.
  - **Navigation Button:**
    - Includes a button that navigates the user to the orders screen, allowing them to view their order history.


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
