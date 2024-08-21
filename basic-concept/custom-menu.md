# Creating Custom Menus in WordPress

Custom menus in WordPress let you create and manage navigation menus that can be displayed in different locations on your site. This guide will walk you through the steps to create and customize custom menus.

## 1. Registering a Custom Menu Location

Before you can display a custom menu, you need to register a menu location in your theme.

### 1.1. Add Code to `functions.php`

1. **Open your theme’s `functions.php` file** (located in your theme directory: `wp-content/themes/your-theme/functions.php`).

2. **Add the Following Code**:

   ```php
   <?php
   // Register Custom Menus
   function register_custom_menus() {
       register_nav_menus(array(
           'primary'   => __('Primary Menu', 'textdomain'),
           'footer'    => __('Footer Menu', 'textdomain'),
       ));
   }
   add_action('init', 'register_custom_menus');
   ```



## 2. Adding a Custom Menu
Once you have registered a menu location, you can create and assign a custom menu through the WordPress admin interface.

### 2.1. Create a Custom Menu
- Log in to Your WordPress Admin Dashboard.

- Go to Appearance > Menus.

- Click “Create a New Menu”:

- Menu Name: Enter a name for your menu (e.g., "Main Menu").
- Click “Create Menu”.
- Add Items to Your Menu:

    - Pages: Select pages from the left column and click “Add to Menu.”
    - Posts: Select posts to add.
    - Custom Links: Enter URLs and link text to create custom links.
    - Categories: Add categories to the menu.
- Organize Menu Items:

    - Drag and Drop: Arrange the menu items in the desired order.
    - Submenus: Drag items slightly to the right to create dropdown submenus.
- Save Menu: Click “Save Menu” to save your changes.

## 2.2. Assign Menu to a Location
In the same Menus screen, find the "Menu Settings" section.

### Select Display Location:

- Primary Menu: Assign the menu to the "Primary Menu" location.
- Footer Menu: Assign the menu to the "Footer Menu" location (or any other registered location).
- Click “Save Menu” to apply the changes.

## 3. Displaying the Menu in Your Theme
To display the custom menu in your theme, you need to use the wp_nav_menu function in your theme’s template files.

### 3.1. Add Code to Your Theme Files
Open the theme file where you want to display the menu (e.g., header.php, footer.php, or a sidebar file).

Add the Following Code:

```php
<?php
// Display Primary Menu
wp_nav_menu(array(
    'theme_location' => 'primary',
    'container'      => 'nav',
    'container_class' => 'primary-menu-class',
    'menu_class'     => 'menu',
    'fallback_cb'    => false,
));
?>

<?php
// Display Footer Menu
wp_nav_menu(array(
    'theme_location' => 'footer',
    'container'      => 'nav',
    'container_class' => 'footer-menu-class',
    'menu_class'     => 'menu',
    'fallback_cb'    => false,
));
?>
```

#### Explanation
- 'theme_location': Specifies the registered menu location to display.
- 'container': Defines the HTML element to wrap the menu (e.g., nav, div).
- 'container_class': Adds a CSS class to the container element.
- 'menu_class': Adds a CSS class to the <ul> element of the menu.
'fallback_cb': Disables the default fallback menu if no menu is assigned.

## 4. Customizing the Menu Appearance
You can style your custom menu using CSS. Add custom styles to your theme’s stylesheet (style.css).

```php 
/* Primary Menu Styles */
.primary-menu-class {
   background-color: #333;
}

.primary-menu-class .menu {
   list-style: none;
   margin: 0;
   padding: 0;
}

.primary-menu-class .menu li {
   display: inline;
   margin-right: 20px;
}

.primary-menu-class .menu li a {
   color: #fff;
   text-decoration: none;
}

/* Footer Menu Styles */
.footer-menu-class {
   background-color: #222;
}

.footer-menu-class .menu {
   list-style: none;
   margin: 0;
   padding: 0;
}

.footer-menu-class .menu li {
   display: inline;
   margin-right: 15px;
}

.footer-menu-class .menu li a {
   color: #ddd;
   text-decoration: none;
}
```

## Additional Tips
Menu Management: Use the WordPress admin interface to manage menus, add items, and assign them to different locations.
Theme Development: When developing themes, ensure that menu locations are registered and menus are displayed correctly.