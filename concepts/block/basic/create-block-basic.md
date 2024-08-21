# Create custom wordpress block

Creating a custom WordPress block involves several steps. You need to use the WordPress Block Editor (Gutenberg) and typically work with JavaScript, particularly React, along with PHP. Below is a step-by-step guide to creating a custom block.

### Prerequisites

1. **WordPress Installed**: Ensure you have a WordPress installation set up.
2. **Node.js and npm**: Install Node.js and npm if you haven't already.

### Steps to Create a Custom WordPress Block

#### 1. Set Up Your Environment

1. **Install and Activate the Gutenberg Plugin (Optional)**: For the latest block editor features, you might need to install the Gutenberg plugin from the WordPress plugin repository, although the Block Editor is now part of WordPress core.

2. **Create a Plugin Folder**: Navigate to your `wp-content/plugins` directory and create a new folder for your custom block, e.g., `my-custom-block`.

3. **Create Plugin Files**: Inside your plugin folder, create the following files:

   - `my-custom-block.php`
   - `package.json`
   - `src/index.js`
   - `src/editor.scss`
   - `src/style.scss`

#### 2. Set Up Your Plugin File

Open `my-custom-block.php` and add the following code:

```php
<?php
/**
 * Plugin Name: My Custom Block
 * Description: A custom block for WordPress.
 * Version: 1.0.0
 * Author: Your Name
 * License: GPL2
 */

defined('ABSPATH') || exit;

function my_custom_block_register_block() {
    wp_register_script(
        'my-custom-block-editor',
        plugins_url('src/index.js', __FILE__),
        array('wp-blocks', 'wp-element', 'wp-editor'),
        filemtime(plugin_dir_path(__FILE__) . 'src/index.js')
    );

    wp_register_style(
        'my-custom-block-editor-styles',
        plugins_url('src/editor.scss', __FILE__),
        array('wp-edit-blocks'),
        filemtime(plugin_dir_path(__FILE__) . 'src/editor.scss')
    );

    wp_register_style(
        'my-custom-block-frontend-styles',
        plugins_url('src/style.scss', __FILE__),
        array(),
        filemtime(plugin_dir_path(__FILE__) . 'src/style.scss')
    );

    register_block_type('my-custom-block/my-block', array(
        'editor_script' => 'my-custom-block-editor',
        'editor_style'  => 'my-custom-block-editor-styles',
        'style'         => 'my-custom-block-frontend-styles',
    ));
}

add_action('init', 'my_custom_block_register_block');
```

This file registers the block and its associated JavaScript and CSS files.

#### 3. Set Up JavaScript for Your Block

Open `src/index.js` and add the following code:

```js
import { registerBlockType } from '@wordpress/blocks';
import { PlainText } from '@wordpress/block-editor';
import './editor.scss';

registerBlockType('my-custom-block/my-block', {
    title: 'My Custom Block',
    icon: 'smiley',
    category: 'common',

    attributes: {
        content: {
            type: 'string',
            source: 'text',
            selector: 'p',
        },
    },

    edit({ attributes, setAttributes }) {
        const { content } = attributes;

        return (
            <div className="my-custom-block">
                <PlainText
                    value={content}
                    onChange={(value) => setAttributes({ content: value })}
                    placeholder="Enter text..."
                />
            </div>
        );
    },

    save({ attributes }) {
        const { content } = attributes;

        return (
            <div className="my-custom-block">
                <p>{content}</p>
            </div>
        );
    },
});
```

This code defines a block with editable text. The `edit` function specifies how the block should be rendered in the editor, and the `save` function specifies how it should appear on the frontend.

#### 4. Style Your Block

Open `src/editor.scss` and `src/style.scss` to add custom styles for the block in the editor and frontend.

For `src/editor.scss`:

```scss
.my-custom-block {
    padding: 20px;
    border: 1px solid #ddd;
}
```

For `src/style.scss`:

```scss
.my-custom-block {
    background-color: #f9f9f9;
    padding: 10px;
    border-radius: 4px;
}
```

#### 5. Set Up npm

In the root of your plugin folder, run `npm init` to create a `package.json` file. Then install the necessary dependencies:

```bash
npm install @wordpress/browsersync @wordpress/scripts --save-dev
```

You can use `@wordpress/scripts` to handle JavaScript transpiling and bundling. 

#### 6. Add Build Scripts

Update your `package.json` to include build scripts:

```json
{
    "name": "my-custom-block",
    "version": "1.0.0",
    "private": true,
    "dependencies": {},
    "devDependencies": {
        "@wordpress/browsersync": "^1.0.0",
        "@wordpress/scripts": "^24.0.0"
    },
    "scripts": {
        "build": "wp-scripts build",
        "start": "wp-scripts start"
    }
}
```

Run `npm run build` to compile your JavaScript and CSS files.

#### 7. Activate Your Plugin

Go to the WordPress admin dashboard, navigate to the Plugins section, and activate your custom block plugin.

### Testing Your Block

Once activated, go to the Block Editor and add your custom block to a post or page. You should see it with the specified functionality and styles.

Congratulations! You’ve created a custom WordPress block. You can now customize it further or add additional functionality as needed.


## Online Generator

https://create-wp-blocks.com/