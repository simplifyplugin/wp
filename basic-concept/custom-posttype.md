# Creating a Custom Post Type and Taxonomy in WordPress

In WordPress, custom post types and taxonomies allow you to organize content in ways that go beyond standard posts and pages. This guide will help you create both a custom post type and a custom taxonomy.

## 1. Creating a Custom Post Type

Custom post types are used to create content types that are different from the default posts and pages. For example, you might want to create a custom post type for "Books," "Movies," or "Events."

### 1.1. Add Code to `functions.php`

1. **Open your theme’s `functions.php` file** (located in your theme directory) or create a custom plugin to add the code.

2. **Add the Following Code**:

   ```php
   <?php
   // Register Custom Post Type
   function create_custom_post_type() {
       $labels = array(
           'name'               => _x('Books', 'post type general name', 'textdomain'),
           'singular_name'      => _x('Book', 'post type singular name', 'textdomain'),
           'menu_name'          => _x('Books', 'admin menu', 'textdomain'),
           'name_admin_bar'     => _x('Book', 'add new on admin bar', 'textdomain'),
           'add_new'            => _x('Add New', 'book', 'textdomain'),
           'add_new_item'       => __('Add New Book', 'textdomain'),
           'new_item'           => __('New Book', 'textdomain'),
           'edit_item'          => __('Edit Book', 'textdomain'),
           'view_item'          => __('View Book', 'textdomain'),
           'all_items'          => __('All Books', 'textdomain'),
           'search_items'       => __('Search Books', 'textdomain'),
           'parent_item_colon'  => __('Parent Books:', 'textdomain'),
           'not_found'          => __('No books found.', 'textdomain'),
           'not_found_in_trash' => __('No books found in Trash.', 'textdomain'),
       );
       
       $args = array(
           'labels'             => $labels,
           'public'             => true,
           'publicly_queryable' => true,
           'show_ui'            => true,
           'show_in_menu'       => true,
           'query_var'          => true,
           'rewrite'            => array('slug' => 'books'),
           'capability_type'    => 'post',
           'has_archive'        => true,
           'hierarchical'       => false,
           'menu_position'      => 5,
           'supports'           => array('title', 'editor', 'thumbnail', 'excerpt', 'comments'),
       );
       
       register_post_type('book', $args);
   }
   add_action('init', 'create_custom_post_type');
   ```

   ### Online Post Type

   https://generatewp.com/post-type/