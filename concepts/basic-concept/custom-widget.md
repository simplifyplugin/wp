# Creating a Custom Widget in WordPress

Custom widgets in WordPress enable you to add new types of content to your sidebar or other widget areas. This guide will walk you through creating a custom widget.

## 1. Create a Custom Widget Class

To create a custom widget, you’ll need to define a new class that extends the `WP_Widget` class. This class will define the widget’s behavior and appearance.

### 1.1. Add Code to `functions.php`

1. **Open Your `functions.php` File**

   - **Location**: This file is located in your theme directory: `wp-content/themes/your-theme/functions.php`.
   - **Alternative**: You can also create a custom plugin to add this code.

2. **Add the Following Code**

   ```php
   <?php
   // Register Custom Widget
   function register_custom_widget() {
       register_widget('Custom_Widget');
   }
   add_action('widgets_init', 'register_custom_widget');

   // Define Custom Widget Class
   class Custom_Widget extends WP_Widget {

       // Constructor
       function __construct() {
           $widget_options = array(
               'classname' => 'custom_widget',
               'description' => 'A custom widget for displaying custom content',
           );
           parent::__construct('custom_widget', 'Custom Widget', $widget_options);
       }

       // Widget Output
       public function widget($args, $instance) {
           echo $args['before_widget'];

           // Check if the title is set
           if (!empty($instance['title'])) {
               echo $args['before_title'] . esc_html($instance['title']) . $args['after_title'];
           }

           // Display the custom content
           echo '<p>' . esc_html($instance['content']) . '</p>';

           echo $args['after_widget'];
       }

       // Widget Backend Form
       public function form($instance) {
           $title = !empty($instance['title']) ? $instance['title'] : '';
           $content = !empty($instance['content']) ? $instance['content'] : '';
           ?>
           <p>
               <label for="<?php echo $this->get_field_id('title'); ?>">Title:</label>
               <input class="widefat" id="<?php echo $this->get_field_id('title'); ?>" name="<?php echo $this->get_field_name('title'); ?>" type="text" value="<?php echo esc_attr($title); ?>">
           </p>
           <p>
               <label for="<?php echo $this->get_field_id('content'); ?>">Content:</label>
               <textarea class="widefat" id="<?php echo $this->get_field_id('content'); ?>" name="<?php echo $this->get_field_name('content'); ?>" rows="5"><?php echo esc_textarea($content); ?></textarea>
           </p>
           <?php
       }

       // Update Widget Options
       public function update($new_instance, $old_instance) {
           $instance = array();
           $instance['title'] = (!empty($new_instance['title'])) ? sanitize_text_field($new_instance['title']) : '';
           $instance['content'] = (!empty($new_instance['content'])) ? sanitize_textarea_field($new_instance['content']) : '';
           return $instance;
       }
   }
