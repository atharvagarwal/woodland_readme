
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
├── app/                     # Automatic routing is done
│   ├── _layout.tsx          # Layout of the app
│   ├── auth/                # Initial entry point of the app in logged in state
│   │   ├── _layout.tsx      # Default layout for logged in state
│   │   ├── Explore.tsx      # Page for exploring
│   │   └── Cart.tsx         # Cart page
│   ├── index.tsx            # Home page
│   ├── Otp.tsx              # OTP page
│   ├── SignIn.tsx           # Sign-in page
│   ├── tabs/                # Initial entry point of the app in not logged in state
│   │   ├── _layout.tsx      # Default layout for not logged in state
│   │   ├── Cart.tsx         # Cart page (tabs)
│   │   ├── Categories.tsx   # Categories page
│   │   ├── Explore.tsx      # Explore page
│   │   ├── home.tsx         # Home page (tabs)
│   │   ├── Orders.tsx       # Orders page
│   ├── +native-intent.tsx   # Native intent handling
│   ├── +not-found.tsx       # 404 Not Found page
│   ├── Checkout.tsx         # Checkout page
│   ├── OrderDetail.tsx      # Order details page
│   ├── ProductDetail.tsx    # Product details page
│   └── Success.tsx          # Success page
├── assets/
│   ├── images/              # Folder for app images
│   └── fonts/               # Folder for app fonts
├── components/             # Folder for reusable components
│   ├── base
│   │   ├── Button.tsx       # Base button component
│   │   └── Header.tsx       # Base header component
│   ├── cart
│   │   └── Card.tsx         # Cart card component
│   ├── checkout
│   │   ├── Address.tsx      # Address component
│   │   ├── AddressForm.tsx  # Address form component
│   │   ├── Bill.tsx         # Bill component
│   │   ├── Discount.tsx     # Discount component
│   │   └── Donation.tsx     # Donation component
│   ├── common
│   │   └── form
│   │       └── ControlledInput.tsx # Controlled input component
│   ├── orders
│   │   ├── OrderList.tsx    # Order list component
│   │   ├── OrderDetails.tsx # Order details component
│   │   └── OrderHistory.tsx # Order history component
│   ├── products
│   │   ├── ProductList.tsx  # Product list component
│   │   ├── ProductDetails.tsx # Product details component
│   │   └── ProductSearch.tsx  # Product search component
│   └── tests
│       └── styledtext-test.js # Tests for styled text components
└── utilities/
    └── securityClient.ts    # Utility for security-related client operations
hooks/api/
├── auth/
│   ├── index.tsx
│   ├── queries.tsx
│   ├── types.ts
├── checkout/
│   ├── index.tsx
│   ├── query.tsx
│   ├── types.ts
├── order/
│   ├── queries.tsx
│   ├── types.ts
├── product/
│   ├── index.tsx
│   ├── queries.tsx
│   ├── types.ts
├── reactQuery.tsx
├── types.tsx
│
├── store/
│   └── store.ts              # State management files based on Zustand
├── utils/
│   └── rules.ts              # Form validation rules and utility functions
│
├── config/
│   └── config.ts             # Configuration settings for environment variables, API keys, and other libraries for axios etc
├── constants/
│   └── colors.ts             # contains color scheme for our app
│   └── fonts.ts             # contains font size and weight for our app
```

## App Folder Breakdown


## **_layout.tsx**

The `_layout.tsx` component is responsible for providing a structured container for rendering screens throughout the app.

- **SafeAreaView:**
  - Ensures content avoids system UI elements like the status bar or notch, maintaining a clean and accessible layout.
- **Slot Component:**
  - Serves as a placeholder for dynamically rendering child routes or screens, allowing for flexible navigation and screen transitions.
- **Styles:**
  - Uses `styles.top` to apply a background color sourced from `Colors.light.background`.
  - Ensures the view occupies the full height of the screen using `flex: 1`, creating a consistent layout across different screens.

This setup ensures a flexible, visually consistent layout for the app’s navigation structure.

## **(auth) folder breakdown**

## **index.tsx**

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

## **Signin.tsx**

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

## **Otp.tsx**

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




## **(tabs) folder breakdown**
## **Cart**
The **Cart** component includes functionalities and UI elements related to cart management:

- **Empty Cart**: 
  - Displays a message "Your cart is empty" with a "Shop Now" button that navigates to the home screen when the cart is empty.

- **Cart Items**:
  - Maps over the `cartProduct` array and renders each item as a `CartCard` with product details such as image, title, and price if items are present.

- **Checkout Button**:
  - Includes a "Checkout" button at the bottom that navigates the user to the checkout page.

- **ScrollView**:
  - Uses `ScrollView` for scrolling through cart items, styled for proper alignment and layout.

## **Explore.tsx**
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

## **Home.tsx**
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


## **Orders.tsx**

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

## **+native-intent.tsx**

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



## **+not-found.tsx**

The `+not-found.tsx` component is used to handle scenarios where a requested resource is not found. It provides a fallback mechanism to guide users back to the main part of the app.

**Functionality:**

- **Alert:** Displays an alert with the message "No results found! Returning to home page" when a resource is not found.
- **Redirection:** Uses the `Redirect` component from `expo-router` to navigate the user back to the home page.

**Usage:**

This component is typically used in routing systems to handle 404 errors or cases where a requested resource is unavailable, ensuring that users are redirected to the main page of the app.

## **Checkout.tsx**

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


## **OrderDetail.tsx**

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

## **ProductDetail.tsx**

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



## **Success.tsx**

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



## Components Breakdown

## **/Base/Button**

The `CustomButton` component renders a button with three style options: 'primary', 'secondary', and 'tertiary'. Key features include:

- **Style Options:**
  - **Primary:** A solid button with a background color.
  - **Secondary:** A bordered button with no background.
  - **Tertiary:** A button with no specific style.
- **Props:**
  - **`type` (string):** Defines the button style ('primary', 'secondary', 'tertiary').
  - **`title` (string):** The text displayed on the button.
  - **`onPress` (function):** Callback function triggered when the button is pressed.
- **Functionality:**
  - The button's appearance dynamically adjusts based on the `type` prop, ensuring flexible design and integration across different parts of the app.

## **/Base/Header**

The `Header` component displays a customizable header with search and drawer functionalities. Key features include:

- **Props:**
  - **`title` (string):** The text displayed in the header.
  - **`onExplore` (boolean, optional):** Determines if the Explore functionality is enabled.
- **State Management:**
  - **`searchBar` (boolean):** Controls the visibility of the search bar.
  - **`searchText` (string):** Manages the input text for the search bar.
  - **`drawerPress` (boolean):** Controls the visibility of the drawer modal.
- **Search Bar:**
  - Displays a `TextInput` for search when active, routing to the Explore page based on input.
- **Drawer:**
  - Tapping the drawer icon shows a `DrawerModal` with options for logging out and deleting the account.
- **Icons:**
  - Includes icons for toggling the search bar and navigating to the Cart screen.

This component is well-structured for dynamic title display and navigation functionality, enhancing the app's usability.

## **Cart**

The `CartCard` component represents an item in a shopping cart. Key features include:

- **Props:**
  - **`id` (string):** Unique identifier for the cart item.
  - **`imageUrl` (string):** URL of the item's image.
  - **`title` (string):** Name of the item.
  - **`price` (number):** Price of the item.
  - **`color` (string):** Color of the item.
  - **`size` (string):** Size of the item.
  - **`quantity` (number):** Quantity of the item in the cart.
  - **`pickerEnabled` (boolean):** Determines if the quantity can be updated via a dropdown.
- **Main Features:**
  - **Image Display:** Shows the product image using Expo's `Image` component with a loader (`woodland-loader.gif`).
  - **Details:** Renders the item's title, price, color, size, and quantity.
  - **Quantity Picker:** Allows users to change the quantity via a dropdown if `pickerEnabled` is true. The dropdown toggles between open and closed states.
  - **Remove Functionality:** Users can remove the item from the cart using the `removeFromCart` function.
- **State:**
  - Manages the dropdown state (`open`) to toggle the visibility of the quantity picker.

This component is designed to be flexible and reusable, providing a detailed view of cart items with options to modify the quantity and remove items.



## Checkout Components

## **Address.tsx**

The `AddressCard` component displays a user's address with an option to confirm delivery. Key features include:

- **Props:**
  - **`address` (string):** The address to be displayed.
- **Features:**
  - **Address Display:** Shows a "Home" label and the provided address.
  - **Delivery Button:** Includes a "Deliver to this address" button that logs a message when pressed.
- **Styles:**
  - **Container:** Features a light background with rounded corners, shadows, and elevation, covering 95% of the screen width.
  - **Header:** Displays the "Home" label and address with padding.
  - **Button:** Styled in green with bold white text for the delivery option.

This reusable component is ideal for checkout processes or address books.

## **AddressForm.tsx**

The `AddressForm` component is designed for collecting address details, leveraging `react-hook-form` for form state management and validation. Key features include:

- **Form Fields:**
  - Includes fields for `houseNumber`, `city`, `pin`, `state`, and `landmark`, each managed with `ControlledInput`, a custom component integrated with `react-hook-form`.
- **Validation:**
  - Essential fields (`houseNumber`, `city`, `pin`, `state`) include validation rules to ensure correct input, with custom error messages.
- **Reset Button:**
  - Positioned at the top-right to clear form data when pressed.
- **Layout:**
  - Uses flexbox for responsive arrangement of inputs, with padding, a light background, and a border at the top for visual separation.

This component is useful for adding new addresses, ensuring users provide all necessary information with built-in validation and a reset option.

## **Bill.tsx**

The `Bill` component provides a detailed financial summary. Key features include:

- **Props:**
  - Accepts `subtotal`, `donation`, `discount`, `deliveryCharges`, and `total`.
- **Layout:**
  - Displays each financial item (e.g., subtotal, donation, discount) in its own row with labels and formatted values.
- **Total:**
  - Highlights the final amount at the bottom in bold and larger font.
- **Styling:**
  - Uses a light background with rounded corners and a border for a card-like appearance. Text is formatted for clarity and readability.

This component ensures a clear, organized view of charges and totals for easy user review.

## **Donation.tsx**

The `Donation` component allows users to opt-in for updates and add a donation to their transaction. Key features include:

- **Props:**
  - **`onSelect` (function):** Notifies changes when checkboxes are selected or deselected.
- **State:**
  - **`receiveUpdates` (boolean):** Tracks user preference for receiving updates.
  - **`addDonation` (boolean):** Manages if a ₹30 donation should be added to the transaction.
- **Checkboxes:**
  - **Updates Checkbox:** Lets users opt-in for updates on products and promotions.
  - **Donation Checkbox:** Allows users to add a ₹30 donation, triggering `onSelect` when changed.
- **Styles:**
  - Features a light background and aligns checkboxes with labels for a clear and user-friendly layout.

This component enhances the checkout process by offering users the option to contribute to donations and receive updates.


## **ControlledInput**

The `ControlledInput` component integrates with React Hook Form to offer a versatile input field with enhanced functionalities.

- **Props:**
  - **`icon` (React.Element):** Optional visual icon to display inside the input field.
  - **`name` (string):** Name of the form field, used for form state management.
  - **`rules` (object):** Validation rules for the input field.
  - **`control` (object):** React Hook Form control object used for managing form state.
  - **`containerStyle` (object):** Custom styles for the overall container of the input field.
  - **`rootContainerStyle` (object):** Styles for the root container wrapping the input field.
  - **`inputContainerStyle` (object):** Styles for the container specifically around the input.
  - **`isPassword` (boolean):** Determines if the input field should handle password visibility.
  - **`countryCode` (string):** Handles the display and selection of country codes (optional).
  - **`onCountryChange` (function):** Callback function triggered when the country code changes.

- **State Management:**
  - **`secureText` (boolean):** Manages password visibility, toggling between showing and hiding password characters.

- **Controller Integration:**
  - Utilizes React Hook Form's `Controller` to seamlessly bind form state and handle validation. The `Controller` component manages field value and error state, ensuring smooth integration with the form.

- **Rendering:**
  - Renders a `TextInput` component with optional password visibility toggle using an Ionicons icon.
  - Displays error messages if validation fails.
  - Applies custom styles provided through props to adjust the appearance and layout of the input field.

This component is designed for flexibility, supporting various input types and customizations while efficiently handling form validation and state management.


## **ProductDetail**

## **PincodeChecker.tsx**

The `PincodeChecker` component handles pincode input with validation.

- **Key Features:**

  - **Props:**
    - **`onPress` (function):** Callback triggered when the "Check" button is pressed.
    - **`control` (object):** React Hook Form’s `Control` object for managing form state and validation.
    - **`name` (string):** Name of the form field used by React Hook Form.
    - **`maxLength` (number, optional):** Limits the pincode input length.

  - **Components:**
    - **`ControlledInput`**: A custom input field integrated with React Hook Form, styled specifically for pincode entry.
    - **`TouchableOpacity`**: A button labeled "Check", which triggers the `onPress` function.

  - **Styles:**
    - **`pincodeContainer`**: Flex container used for layout.
    - **`pincodeButtonContainer`**: Contains the `ControlledInput`.
    - **`checkButton`**: Styled button for submission.

  - **Usage:**
    - Ideal for scenarios requiring pincode input, such as code verification or delivery checks.

## **ProductCarousel.tsx**

The `ProductCarousel` component displays a horizontal image carousel with pagination indicators.

- **Key Features:**

  - **Props:**
    - **`images` (array):** Array of image URLs to be displayed in the carousel.

  - **Components:**
    - **`Img`**: Renders each image with a loading indicator.
    - **`FlatList`**: Displays images horizontally, with paging enabled.
    - **`ActivityIndicator`**: Shows a loading spinner while images are being loaded.

  - **Functionality:**
    - **Image Handling**: Displays images in a scrollable carousel. An `ActivityIndicator` is shown while images are loading.
    - **Pagination**: Dots below the carousel indicate the current image. The opacity of the active dot changes based on the currently visible image.

  - **Styles:**
    - **`dotContainer`**: Container for pagination dots.
    - **`dot`**: Style for pagination dots, with variable opacity to reflect the currently visible image.

  - **Usage:**
    - Ideal for displaying multiple images in a scrollable format, with visual indicators for the current image.


## **Orders Breakdown**

## **OrderCard.tsx**

The `OrderCard` component displays the details of an order with options to view or cancel it.

- **Key Features:**

  - **Props:**
    - **`imageUrl` (string):** Image source for the product.
    - **`title` (string):** Product title.
    - **`subtitle` (string):** Quantity of the product.
    - **`size` (string):** Size of the product.
    - **`orderId` (string):** Identifier for the order.
    - **`subOrderId` (string):** Identifier for the sub-order.
    - **`cancellable` (boolean):** Determines if the order can be canceled.
    - **`status` (string):** Current status of the order.

  - **Components:**
    - **`Image`**: Displays the product image with a placeholder and caching.
    - **`ActivityIndicator`**: Shows a spinner while the order is being canceled.
    - **`TouchableOpacity`**: Buttons for viewing order details and canceling the order.

  - **Functionality:**
    - **View Details**: Navigates to the order detail page.
    - **Cancel Order**: Prompts for confirmation and cancels the order if confirmed. Updates the order list and handles errors.

  - **Styles:**
    - **`Container`**: Card with shadow and padding for the order.
    - **`Row`**: Layout for image and details.
    - **`Button`**: Styled for "View Details" and "Cancel" actions.

  - **Usage:**
    - This component is used to present individual order details with actions to view more information or cancel the order, depending on its status.

## **OrderDetailCard.tsx**

The `OrderDetailCard` component displays detailed information about an individual order item.

- **Key Features:**

  - **Props:**
    - **`url` (string):** Image URL of the product.
    - **`title` (string):** Product title.
    - **`color` (string):** Color of the product.
    - **`quantity` (number):** Quantity ordered.
    - **`size` (string):** Size of the product.
    - **`price` (number):** Original price of the product.
    - **`finalPrice` (number):** Discounted or final price.
    - **`subOrderId` (string):** Unique identifier for the sub-order.

  - **Components:**
    - **`Image`**: Displays the product image.
    - **`Text`**: Shows product details such as title, color, size, quantity, and price.

  - **Functionality:**
    - **Price Display**: Shows the original price with a line-through if it differs from the final price. Displays the final price prominently.

  - **Styles:**
    - **`Root`**: Card layout with border, padding, and spacing.
    - **`Image Container`**: Section for the product image.
    - **`Product Detail Container`**: Section for product details.
    - **`Price Details Container`**: Section for displaying prices.

  - **Usage:**
    - This component is used to present detailed information about an item in an order, including its image, specifications, and pricing, with clear differentiation between original and final prices.


## **Common Components**


## Accordion.tsx

The `Accordion` component provides a collapsible section for displaying and hiding content.

## Props

- `title` (string): Header text.
- `onLinkPress` (function, optional): Callback function for link press.
- `href` (string, optional): Optional navigation link.
- `children` (node): Content to show when expanded.
- `dropdown` (boolean, default: `true`): Controls the presence of a dropdown arrow.
- `subDrawer` (boolean): Adjusts styling for sub-items.

## Features

- **Toggle Function**: Clicking the header toggles the content visibility.
- **Icon**: An arrow icon indicates the expanded or collapsed state.

## Styles

- `link` and `subLink`: Styles for text and layout based on item type.
- `text` and `subText`: Font styles for header text.

## Usage

Used for creating expandable sections in a UI, ideal for menus or settings.



## CategoryButton.tsx

The `CategoryButton` component is a customizable button for React Native.

## Props

- `text` (string): Button label.
- `onPress` (function): Function to call when the button is pressed.
- `backgroundColor` (string): Button background color.
- `textColor` (string): Text color.
- `id` (string): Unique identifier for the button.

## Features

- **Style**: Uses `Pressable` for handling press events and supports custom colors for background and text.
- **Layout**: Styled with rounded corners and center-aligned text.

## Usage

Ideal for interactive elements where customization of colors and text is needed, such as category filters or action buttons.



## CategoryList.tsx

The `CategoryList` component is a horizontal scrollable list of category buttons.

## Features

- **Data Handling**: Renders buttons using an array of category names.
- **State Management**: Tracks the selected category with `selectedId` and updates it on button press.
- **Navigation**: Uses `useRouter` from `expo-router` to navigate to a category-specific page.

## Components

- **ScrollView**: Allows horizontal scrolling of category buttons. Styled for proper height and background color.
- **CategoryButton**: Custom button component that updates appearance based on selection.

## Usage

Displays a list of categories with the ability to select and view related content. The selected category is highlighted, and pressing a button navigates to a category-specific page.



## drawerModal.tsx

The `DrawerModal` component creates a modal drawer for navigation and settings.

## Features

- **Visibility**: Controlled via the `visible` prop.
- **Content**: Includes a close button, logo, and a list of navigational links organized into expandable accordions.

## Usage

Provides a detailed navigation menu and settings options within an app, supporting hierarchical categories and conditional content based on the platform.

## FilterComponent.tsx

The `FilterComponent` provides a flexible and reusable interface for applying and resetting filters.

## Props

- `handleCancelFilters` (function): Resets all filters.

## Functionality

- Integrates with a state management system to update and apply filters dynamically.

## Usage

Designed to be flexible and reusable, allowing integration with various state management systems for dynamic filter updates.



## ProductListingCard.tsx

The `ProductListingCard` displays a product card featuring an image, title, pricing, and color options.

## Props

- `title` (string): Product title.
- `price` (number): Original price.
- `offerPrice` (number): Discounted price.
- `productImageUrl` (string): URL for the main product image.
- `productMeta` (object): Color options with URLs.

## Functionality

- Displays the main product image and a discount badge if applicable.
- Shows both original and discounted prices.
- Renders clickable color thumbnails that update the main image and navigate to product details.

## Navigation

- Uses `expo-router` to change routes based on the selected color's slug.

## Usage

Ideal for displaying product details with interactive color options and pricing information.



## Size.tsx

The `Size` component displays a size option with customizable styling based on availability and state.

## Props

- `size` (string): Size text to display.
- `soldOut` (boolean, optional): Indicates if the size is unavailable.
- `color` (string): Background color of the size option.
- `inCart` (boolean, optional): Indicates if the size is in the cart.

## Functionality

- Displays a circular box with the size text.
- Applies different styles for sizes marked as sold out or those in the cart:
  - **Sold Out**: Gray background and white text.
  - **In Cart**: White text.
  - **Available**: Black text and background color as specified.

## Styling

- `root`: Basic style for available sizes.
- `soldRoot`: Style for sizes marked as sold out.

## Usage

Used for displaying size options with visual cues for availability and cart status.


## SizeChart.tsx

The `SizeChart` component displays a modal with size charts for shoes or garments based on the `type` prop.

## Props

- `visible` (boolean): Controls the visibility of the modal.
- `type` (string): Determines the chart type, either `"SHOES"` or `"GARMENTS"`.
- `onCrossPress` (function, optional): Function called when the close button is pressed.

## Functionality

- Displays size charts for different categories:
  - **Garments**: Men's and women's tops and bottoms.
  - **Shoes**: Men's and women's shoes.
- Each chart includes size measurements in various units (UK, EURO, CM for shoes; chest measurements for garments).
- Alternates row colors for better readability.

## Styling

- Uses `SafeAreaView` for proper layout.
- Includes a close button using Entypo and adjusts text and background colors based on the chart type.

## Usage

Provides size charts for both garments and shoes, with proper styling and visibility control.

## **Constants**

# Color Theme Configuration

This file contains color theme settings for the application, which define the colors used for light and dark modes as well as common elements across the app.

## Color Definitions

### Light Theme

- **Text**: `#000` (Black) - The color used for text in light mode.
- **Background**: `#fff` (White) - The background color in light mode.
- **Tint**: `#2f95dc` - The primary tint color used for highlighting elements.
- **Tab Icon Default**: `#ccc` (Light Gray) - The default color for tab icons.
- **Tab Icon Selected**: `#2f95dc` - The color for selected tab icons.

### Dark Theme

- **Text**: `#fff` (White) - The color used for text in dark mode.
- **Background**: `#15151B` - The background color in dark mode.
- **Tint**: `#fff` (White) - The primary tint color used for highlighting elements in dark mode.
- **Tab Icon Default**: `#ccc` (Light Gray) - The default color for tab icons.
- **Tab Icon Selected**: `#fff` (White) - The color for selected tab icons.
- **Margin**: `#606060` (Gray) - The color used for margins and spacing elements.

### Common Colors

- **Primary Button**: `#00642E` - The color used for primary buttons.
- **PlaceHolder**: `#ADADAD` (Light Gray) - The color for placeholder text.
- **White**: `#fff` - The color white used in various components.
- **Helper**: `#247FF5` - The color used for helper text or elements.
- **Card Background**: `#F6F8FB` - The background color for cards.
- **Default**: `#808080` (Gray) - A default gray color used in various places.
- **Product Card**: `#EAEAEA` - The background color for product cards.

These color settings are used throughout the application to maintain a consistent visual style. The light and dark themes allow the app to adapt to different user preferences or system settings.

# Font Size and Weight Configuration

This file defines the font size and weight settings used throughout the application. These settings help maintain consistent typography and ensure that text elements are appropriately styled.

## Font Sizes

The `size` object specifies various font sizes for different text elements:

- **`xxxs`**: `8` - Extra extra extra small text.
- **`xs`**: `10` - Extra small text.
- **`s`**: `12` - Small text.
- **`default`**: `14` - Default text size.
- **`md`**: `16` - Medium text.
- **`lg`**: `20` - Large text.
- **`xlg`**: `22` - Extra large text.
- **`xxlg`**: `26` - Extra extra large text.
- **`xxxlg`**: `36` - Extra extra extra large text.
- **`large`**: `75` - Used for very large text (e.g., headings or banners).

## Font Weights

The `weight` object defines various font weights that can be applied to text elements:

- **`full`**: `'900'` - Extra bold or heavy text.
- **`semi`**: `'600'` - Semi-bold text.
- **`bold`**: `'bold'` - Bold text.
- **`normal`**: `'normal'` - Normal weight text.
- **`thin`**: `'400'` - Thin or light text.

### Usage

- **Font Sizes**: Use the `size` values to apply consistent font sizes across different text elements. For example, you might use `size.md` for medium-sized text or `size.large` for large headings.
- **Font Weights**: Use the `weight` values to adjust the thickness of text. For instance, `weight.bold` can be used for emphasis or important text, while `weight.thin` can be used for lighter, less prominent text.

These configurations ensure a uniform appearance and help in maintaining a consistent typographic style throughout the application.

## **Store (Using Zustand)**

# Zustand Store Setup

This document provides a detailed breakdown of the Zustand store setup used in the application. Zustand is a lightweight state management library that helps in managing application state efficiently.

## Table of Contents

## 1. Imports and Dependencies

- **`create`**: Function from Zustand to create the store.
- **`persist`, `createJSONStorage`, `StateStorage`**: Middleware functions and types for state persistence using AsyncStorage.
- **`AsyncStorage`**: Local storage for React Native to persist and retrieve state data.

## 2. Type Definitions

- **`ProductProps`**: Defines the shape of a product object.
  - `id`: Unique identifier for the product.
  - `title`: Name of the product.
  - `price`: Regular price of the product.
  - `offerPrice`: Discounted price of the product.
  - `color`: Color of the product.
  - `url`: URL for the product image.
  - `size`: Size of the product.

- **`CartProduct`**: Extends `ProductProps` with additional fields for cart management.
  - `totalPrice`: Total price of the product in the cart.
  - `quantity`: Quantity of the product in the cart.

- **`UserType`**: Represents user information.
  - `firstName`: Optional first name of the user.
  - `lastName`: Optional last name of the user.
  - `email`: Optional email of the user.
  - `phone`: Mandatory phone number of the user.
  - `id`: Mandatory unique identifier for the user.

- **`FilterState`**: Manages filter options for the product list.
  - `selectedCategory`: The selected category for filtering products.
  - `filterOptions`: Options for filtering products.

- **`StoreType`**: Combines all state slices and methods into a single interface.
  - Includes user state, cart state, and filter state.

## 3. Custom AsyncStorage Interface

- **`myAsyncStorage`**: Custom implementation of `StateStorage` that wraps React Native’s `AsyncStorage`.
  - Provides methods to get, set, and remove items from storage.

## 4. Zustand Store Configuration

### Store Initialization

Uses the `create` function from Zustand to initialize the store with persistence middleware.

### State Management

The store manages several pieces of state:

- **User State**:
  - `phone`: User's phone number.
  - `currentUser`: Details of the current user.
  - `isLoading`: Indicates if the application is loading user data.

- **Cart State**:
  - `cartProduct`: Array of products in the cart.
  - `totalAmount`: Total price of all items in the cart.

- **Filters State**:
  - Manages the filtering of products based on selected category and options.

### Actions

- **`addToCart`**: Adds a product to the cart. If the product already exists, increases the quantity.
- **`decreaseQuantity`**: Decreases the quantity of a product in the cart.
- **`increaseQuantity`**: Increases the quantity of a product in the cart.
- **`removeFromCart`**: Removes a product from the cart.
- **`resetCart`**: Clears the cart and resets the total amount.

- **Filter Actions**:
  - `setSelectedCategory`: Sets the selected category for filtering products.
  - `setSelectedFilterOptions`: Sets the selected filter options.
  - `resetFilters`: Resets all filters to default.

### Persistence Configuration

- **`name`**: Identifier for the storage key.
- **`storage`**: Uses `createJSONStorage` with the custom `myAsyncStorage` to persist data.
- **`partialize`**: Defines which parts of the state should be persisted:
  - `cartProducts`
  - `totalAmount`
  - `phone`
- **`onRehydrateStorage`**: Callback that sets the hydration state when the store is rehydrated from storage.

## Conclusion

This Zustand store setup provides an efficient and persistent state management solution for the application. It ensures that user data, cart contents, and filter options are preserved across sessions, enhancing the overall user experience.


##Utils/rules.ts

# Validation Rules

This document outlines the validation rules for user input fields, including passwords, credentials, and email addresses. These rules ensure that user data conforms to expected formats and requirements.

## 1. Password Validation Rule

The password validation rule ensures that passwords meet specific security requirements:

- **`required`**: `'password is required'`
  - This message is shown if the password field is left empty.
  
- **`minLength`**: `{ value: 8, message: 'password must be at least 8 characters long' }`
  - The password must be at least 8 characters long.
  
- **`pattern`**: `{ value: /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/, message: 'password must contain at least one uppercase letter, one lowercase letter, one number and one special character' }`
  - The password must include:
    - At least one lowercase letter
    - At least one uppercase letter
    - At least one digit
    - At least one special character from the set `@$!%*?&`
  - This regular expression enforces these requirements for password security.

## 2. Credential Validation Rule

The credential validation rule is used for fields that can accept either an email or phone number, with validation criteria similar to the password rule:

- **`required`**: `'email or phone number is required'`
  - This message is shown if the field is left empty.
  
- **`pattern`**: `{ value: /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/, message: 'credential must contain at least one uppercase letter, one lowercase letter, one number and one special character' }`
  - The credential must meet similar requirements as the password:
    - At least one lowercase letter
    - At least one uppercase letter
    - At least one digit
    - At least one special character from the set `@$!%*?&`
  - This ensures that the credential input is formatted securely.

## 3. Email Validation Rule

The email validation rule ensures that the input conforms to a valid email format:

- **`pattern`**: `{ value: /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/, message: 'please enter a valid email format' }`
  - The email must match the regular expression pattern:
    - Consists of alphanumeric characters and some special characters (`._-`) before the `@` symbol.
    - The domain part consists of alphanumeric characters separated by periods.
    - The top-level domain (TLD) must be between 2 to 4 alphabetic characters.

## Exported Rules

The validation rules are exported for use in form validation throughout the application:

```javascript
export { passwordRule, credentialRule, emailRule };
```
# API Request Configuration present in (config.ts)

This document provides an overview of the `config.ts` file, which sets up the configuration for making API requests using Axios. Axios is a popular HTTP client for making requests in JavaScript applications.

## File Overview

The `config.ts` file exports a configured Axios instance for making API requests. The configuration includes base URL and default headers for the requests.

## Axios Instance Configuration

The `apiRequest` instance is created using `axios.create()` and is configured with the following settings:

### 1. Base URL

- **`baseURL`**: `"https://api-v1.capcons.com"`
  - This is the root URL for the API endpoints. All relative paths in the API requests will be appended to this base URL.

### 2. Headers

- **`headers`**: 
  - **`"Content-Type"`**: `"application/json"`
    - Specifies that the content type of the requests is JSON. This header informs the server that the data being sent to it is in JSON format.



