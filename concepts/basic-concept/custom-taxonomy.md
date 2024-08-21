# Creating a Custom Taxonomy in WordPress

Custom taxonomies in WordPress allow you to group and categorize content in custom ways beyond the default categories and tags. This guide will help you create a custom taxonomy for your WordPress site.

## 1. Adding Code to `functions.php`

To create a custom taxonomy, you'll need to add some code to your theme's `functions.php` file or a custom plugin.

### 1.1. Open Your `functions.php` File

- **Location**: This file is located in your theme directory: `wp-content/themes/your-theme/functions.php`.
- **Alternative**: You can also create a custom plugin for adding this code.

### 1.2. Add the Following Code

```php
<?php
// Register Custom Taxonomy
function create_custom_taxonomy() {
    $labels = array(
        'name'                       => _x('Genres', 'taxonomy general name', 'textdomain'),
        'singular_name'              => _x('Genre', 'taxonomy singular name', 'textdomain'),
        'search_items'               => __('Search Genres', 'textdomain'),
        'popular_items'              => __('Popular Genres', 'textdomain'),
        'all_items'                  => __('All Genres', 'textdomain'),
        'parent_item'                => __('Parent Genre', 'textdomain'),
        'parent_item_colon'          => __('Parent Genre:', 'textdomain'),
        'edit_item'                  => __('Edit Genre', 'textdomain'),
        'update_item'                => __('Update Genre', 'textdomain'),
        'add_new_item'               => __('Add New Genre', 'textdomain'),
        'new_item_name'              => __('New Genre Name', 'textdomain'),
        'separate_items_with_commas' => __('Separate genres with commas', 'textdomain'),
        'add_or_remove_items'        => __('Add or remove genres', 'textdomain'),
        'choose_from_most_used'      => __('Choose from the most used genres', 'textdomain'),
        'not_found'                  => __('No genres found.', 'textdomain'),
        'menu_name'                  => __('Genres', 'textdomain'),
    );
    
    $args = array(
        'hierarchical'          => true, // Set to false for non-hierarchical (like tags)
        'labels'                => $labels,
        'show_ui'               => true,
        'show_admin_column'     => true,
        'query_var'             => true,
        'rewrite'               => array('slug' => 'genre'),
    );
    
    register_taxonomy('genre', array('book'), $args);
}
add_action('init', 'create_custom_taxonomy');
```

   ### Online Generator
https://generatewp.com/post-type/