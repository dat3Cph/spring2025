---
title: Styling with CSS Modules
description: Exercises for Frontend Week IV
layout: default
nav_order: 1
grand_parent: React IV
parent: Exercises
permalink: /frontend/react-4/exercises/styling-with-css-modules/
---

# Exercise: Styling with CSS Modules in React

1. **Clone the exercise code** from the Coffee Timer Repo:

   ```bash
   git clone --branch nostyling https://github.com/jonbertelsen/coffeetimer
   ```

2. **Install the dependencies** using:

   ```bash
   npm install
   cd coffeetimer
   ```

3. **Run the application** using:

   ```bash
   npm run dev
   ```

   Open your browser and navigate to `http://localhost:5173/` to see the application running.

4. **Consider how to style the application**

   The original application is styled using pure CSS. You can check the [Coffee Timer](https://timer.showcode.dk/) here. The application is responsive to a certain degree, but we want to make it more responsive and modern. We will use **CSS Modules** to style the application. First you should sketch a wireframe of the application. Draw an few boxes and decide which css classes and rules you want to use. Hint: Flexboxl and/or Grid is a good idea.

5. **Make the styling happen**

   Create a CSS component file for the Timer component in the `src/components` folder. For example, if you have a `Timer.jsx` component, create a `Timer.module.css` file in the same directory.

6. **Import the CSS module** into your component file. For example, in `Timer.jsx`, you can import the CSS module like this:

   ```javascript
   import styles from './Timer.module.css';
   ```

   This will allow you to use the styles defined in `Timer.module.css` as an object.

7. **Apply the styles** to your component using the imported `styles` object. For example, if you have a class called `timer` in your CSS module, you can apply it like this:

   ```jsx
   <div className={styles.timer}>
       {/* Timer content */}
   </div>
   ```

   This will ensure that the styles are scoped to this component only, preventing any conflicts with other styles in your application.

8. **Implement light/dark mode**

   Use this [light/dark mode demo](../../../toolbox/react/css-theming.md) as a reference to implement light/dark mode in your application.

   - Create a toggle button to switch between light and dark modes using a state variable.
   - Use CSS variables to define colors for both modes.
   - Update the CSS module to use these variables for styling.

   Hint: See these articles in the Toolbox for more information:

   - [CSS Variables](https://www.w3schools.com/css/css3_variables.asp)
   - [CSS Modules](../../../toolbox/react/css_modules.md)
   - [Light/Dark Mode](../../../toolbox/react/css-theming.md)
   - [Brief explanation of the useContext hook](https://www.youtube.com/watch?v=_HdrLsyAdJg)

9. **Impress your friends**

   - Make sure to test your application in different browsers and devices to ensure it looks good everywhere.
   - Show your application to your friends and ask for feedback on the design and functionality.

10. **Push your code to GitHub**

   Since you started with a git clone from the teachers Repo, you can't push your updated code to your own repository. So do this:

- Remove the `.git` folder in the root of your project. This will remove the git history and connection to the original repository.

   ```bash
   rm -rf .git
   ```

- Create a new repository on GitHub and follow the instructions to push your code to the new repository.
- Make sure to add a README file with a description of your project and how to run it.
