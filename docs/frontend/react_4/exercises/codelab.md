---
title: Codelab 
description: Exercises for Frontend Week IV
layout: default
nav_order: 2
grand_parent: React IV
parent: Exercises
permalink: /frontend/react-4/exercises/codelab/
---

# The Trucking Company

## Practicing styling with CSS Modules, React Router, and error handling

![Codelab](./images/codelab.png){: .x .mx-auto .d-block .my-5 .md .d-md-none .w-50}
![Codelab](./images/codelab.png){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right width="200px"}

This CodeLab exercise is mainly designed to help you practice the concepts you have learned in the Frontend Week IV module. But you will need to use the knowledge from the previous weeks as well.

You will be building a simple application for a trucking company. The application will allow you to manage trucks and drivers. You will be able to view a list of trucks and drivers, register new drivers, and view details about each truck and driver.

![Truck](./images/Truck.png){: .ml-3 .mb-5 .float-right width="200px"}

## The Assignment

### Basic setup with pages

1. Create a new [React application with Vite](../../../toolbox/react/vite.md).
2. Install the react router.
3. Create 2 new folders called `components` and `pages` in the `src` folder.
4. Add the [json Mock server](../../../toolbox/react/json-server.md).
5. Get the `db.json` file from [here](https://gist.githubusercontent.com/Thomas-Hartmann/94381753fbe703ae0da350eaa63cd31d/raw/7560510b42bc8c0cfdf6b4a800b2080269f81601/db.json) and place it in the root of your project.
6. Create the following pages:

   * `Home` page that shows an image of a truck and explains what the app is about (Administering a trucking company).
   * `Trucks` a page that displays a list of trucks. Each truck should have a name and a description with weight and capacity.
   * `Drivers` a page that displays a list of drivers. Each driver should have a name, and a description (with driver details).
   * `RegisterDriver` a page that allows you to register a new driver. Use a form similar to [this example](https://gist.githubusercontent.com/Thomas-Hartmann/94381753fbe703ae0da350eaa63cd31d/raw/c55e1beb132b7725cd1b379ba3fc9590b31c5ba2/form).

### Components

7. Create a `Header` component that displays a navigation bar with links to the different pages.
8. Create a `Footer` component that displays the text "© 2025 Trucking Company".
9. Create a `TruckCard` component that displays a truck with a name, description, and picture. The card should have its own route and be displayed when you click on a truck.
10. Create a `DriverCard` component that displays a driver with a name, description, and picture. The card should have its own route and be displayed when you click on a driver.

### Styling and error handling

11. Style everything using **CSS Modules**. For each component, create a corresponding `.module.css` file (e.g., `TruckCard.module.css`). Use semantic class names like `card`, `title`, `container`, etc.
12. Use global CSS variables in `global.css` to define light/dark theme colors and apply them via the `body` class (e.g. `body.light`, `body.dark`).
13. Add error handling to the `TruckCard` and `DriverCard` components. If the truck or driver does not exist, display an error message in a shared `ErrorBanner` component rendered in the main `Outlet`.
14. Add a 404 page that displays a message saying "Page not found" and a link to the home page.
15. Add a 500 error page that displays a message saying "Server error" when a component fails to render.
16. Use `try-catch` blocks in the fetch logic inside `TruckCard` and `DriverCard` to catch and display errors in the error banner.

### Extra

17. Implement buttons to delete or edit trucks and drivers. The edit button should take you to a form where you can update truck or driver details.

---

**Note:** You are expected to apply your knowledge of **React Context** and **CSS Modules for theming** from the light/dark theme tutorial. See tutorial [here](../../../toolbox/react/css-theming.md).
