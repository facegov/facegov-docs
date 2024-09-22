# Sharing The Layout

FaceGov shares menus, headers, and footers using the layout component pattern. This pattern allows to create a consistent structure across different pages while keeping your code DRY (Don't Repeat Yourself).

A Layout component is used to wrap the content of each page. Here's a breakdown of the key elements:

1. **Header and Footer Components**: These are defined separately and will be consistent across all pages.
2. **Layout Component**: This component wraps the Header, main content area, and Footer. It uses the `children` prop to render the specific page content.
3. **Page Components**: Each page (Home, Profile, Forum, etc.) is defined as a separate component. These components only contain the unique content for that page.
4. **App Component**: This main component sets up the Router and wraps everything in the Layout component. The Routes are defined here, with each Route using the Layout component implicitly.

Benefits of this approach:

1. **Consistency**: The Header and Footer are automatically included on every page.
2. **Flexibility**: You can easily add new pages by creating a new component and adding a new Route in the App component.
3. **Maintainability**: If you need to update the layout, you only need to change the Layout component.
4. **Separation of Concerns**: Each component has a clear, specific purpose.
