# WordPress Practical: Installation and Basic Configuration

## Part 1: Local Installation with XAMPP/WAMP

### Step 1: Set Up XAMPP/WAMP
1. **Download and Install**:
   - Download XAMPP from [Apache Friends](https://www.apachefriends.org/) or WAMP from [WampServer](http://www.wampserver.com/)
   - Run the installer with default settings

2. **Start Services**:
   - Launch XAMPP/WAMP control panel
   - Start Apache and MySQL services

### Step 2: Prepare for WordPress Installation
1. **Download WordPress**:
   - Get the latest version from [wordpress.org](https://wordpress.org/download/)
   - Extract the ZIP file

2. **Set Up Project Folder**:
   - Move extracted WordPress folder to:
     - XAMPP: `C:\xampp\htdocs\your-site`
     - WAMP: `C:\wamp64\www\your-site`

3. **Create Database**:
   - Access phpMyAdmin at `http://localhost/phpmyadmin`
   - Create new database (e.g., `wordpress_db`)
   - Create user with all privileges (remember username/password)

### Step 3: Install WordPress Locally
1. **Run Installation**:
   - Visit `http://localhost/your-site`
   - Select language → Continue

2. **Database Configuration**:
   ```
   Database Name: wordpress_db
   Username: [your created username]
   Password: [your created password]
   Database Host: localhost
   Table Prefix: wp_ (or custom for security)
   ```

3. **Complete Installation**:
   - Run the installation
   - Enter site information:
     - Site Title: "My Local Test Site"
     - Username: (create admin account)
     - Password: (strong password)
     - Email: (your email)
   - Click "Install WordPress"

## Part 2: Remote Installation on Web Server

### Step 1: Prepare Web Hosting
1. **Domain and Hosting**:
   - Purchase domain and hosting (if not already available)
   - Access cPanel or your hosting control panel

2. **Create Database**:
   - In cPanel, go to MySQL Databases
   - Create new database and user
   - Assign user to database with all privileges

### Step 2: Upload WordPress Files
1. **Upload Methods**:
   - **Option 1**: File Manager in cPanel
     - Upload ZIP → Extract in public_html
   - **Option 2**: FTP Client
     - Connect via FTP (FileZilla, WinSCP)
     - Upload files to public_html or subfolder

2. **Install WordPress**:
   - Visit your domain (e.g., `http://yourdomain.com`)
   - Follow same installation process as local setup
   - Use remote database credentials when prompted

## Part 3: Exploring WordPress Directory Structure

Key directories to understand:
```
/wp-admin/          # Admin backend files
/wp-includes/       # Core WordPress files
/wp-content/        # User-generated content
    /themes/        # All installed themes
    /plugins/       # All installed plugins
    /uploads/       # Media library files
```

## Part 4: Navigating the WordPress Dashboard

Main Dashboard Areas:
1. **Left Admin Menu**:
   - Dashboard (Home)
   - Posts (Blog articles)
   - Media (Library)
   - Pages (Static content)
   - Comments
   - Appearance (Themes, menus, widgets)
   - Plugins
   - Users
   - Tools
   - Settings

2. **Top Admin Bar**:
   - Quick access to:
     - Site visit
     - New content (posts, pages, etc.)
     - User profile
     - Updates notifications

## Part 5: Configuring Basic Settings

### 1. General Settings
   - Go to Settings → General
   - Configure:
     - Site Title: "My WordPress Site"
     - Tagline: "Just another WordPress site" (change to your description)
     - WordPress Address (URL): `http://localhost/your-site` (local) or your domain
     - Site Address (URL): Same as above
     - Email Address: (admin email)
     - Membership: (allow user registrations if needed)
     - Timezone: (select your location)
     - Date/Time Format

### 2. Permalink Settings
   - Go to Settings → Permalinks
   - Recommended structure:
     - Select "Post name" (clean URLs like `your-site/sample-post`)
     - Alternative: "Day and name" or "Month and name" for blogs
   - Click "Save Changes"

### 3. User Roles Configuration
   - Go to Users → Add New
   - Create test users with different roles:
     - **Administrator**: Full access
     - **Editor**: Can publish/manage posts
     - **Author**: Can publish own posts
     - **Contributor**: Can write but not publish
     - **Subscriber**: Can only manage profile

## Verification Steps

1. **Local Installation**:
   - Verify you can access `http://localhost/your-site`
   - Check admin dashboard at `http://localhost/your-site/wp-admin`

2. **Remote Installation**:
   - Verify site loads at your domain
   - Check admin dashboard at `yourdomain.com/wp-admin`

3. **Settings Verification**:
   - Visit site frontend - check title/tagline appear
   - Create a test post - check URL structure matches permalink setting
   - Log in as different users - verify role permissions work correctly

## Troubleshooting

Common issues and solutions:
1. **Installation Errors**:
   - Database connection: Verify credentials
   - File permissions: Set wp-content to 755

2. **White Screen**:
   - Enable debug in wp-config.php:
     ```php
     define('WP_DEBUG', true);
     ```

3. **404 Errors**:
   - Save permalinks again
   - Check .htaccess file exists

This completes the practical assignment for installing WordPress both locally and remotely, exploring the directory structure, navigating the dashboard, and configuring basic settings.





# WordPress Practical: Theme Installation and Child Theme Creation

## Step 1: Install and Activate a Free WordPress Theme

1. **Access WordPress Admin Dashboard**
   - Log in to your WordPress admin panel (usually `http://localhost/your-site/wp-admin`)

2. **Install a Free Theme**
   - Go to Appearance → Themes → Add New
   - Browse popular free themes (e.g., Astra, OceanWP, Twenty Twenty-Three)
   - Hover over your chosen theme and click "Install"
   - After installation, click "Activate"

3. **Alternative: Upload Theme ZIP**
   - If you have a theme ZIP file:
     - Go to Appearance → Themes → Add New → Upload Theme
     - Select the ZIP file and click "Install Now"
     - Activate the theme after installation

## Step 2: Customize the Theme Using WordPress Customizer

1. **Access the Customizer**
   - Go to Appearance → Customize

2. **Basic Customizations:**
   - **Site Identity**
     - Upload a logo
     - Set site title and tagline
     - Add site icon (favicon)
   
   - **Colors**
     - Change primary color scheme
     - Adjust background color
     - Modify text/link colors

   - **Typography**
     - Change base font family
     - Adjust font sizes for headings and body text
     - Set line height and letter spacing

   - **Layout Options**
     - Configure container width
     - Set sidebar position (left/right/none)
     - Adjust spacing/padding

3. **Save Changes**
   - Click "Publish" to save all customizations

## Step 3: Create a Child Theme

1. **Create Child Theme Folder**
   - Navigate to `/wp-content/themes/`
   - Create a new folder named `parenttheme-child` (replace "parenttheme" with your theme's name)
     - Example: `twentytwentythree-child`

2. **Create Child Theme Files**
   - Create `style.css` with this header:
     ```css
     /*
     Theme Name:   Twenty Twenty-Three Child
     Theme URI:    http://example.com/twentytwentythree-child/
     Description:  Twenty Twenty-Three Child Theme
     Author:       Your Name
     Author URI:   http://example.com
     Template:     twentytwentythree
     Version:      1.0.0
     License:      GNU General Public License v2 or later
     License URI:  http://www.gnu.org/licenses/gpl-2.0.html
     Text Domain:  twentytwentythree-child
     */
     ```

   - Create `functions.php` with:
     ```php
     <?php
     // Enqueue parent and child theme stylesheets
     add_action('wp_enqueue_scripts', 'my_child_theme_styles');
     function my_child_theme_styles() {
         wp_enqueue_style(
             'parent-theme-style',
             get_template_directory_uri() . '/style.css'
         );
         wp_enqueue_style(
             'child-theme-style',
             get_stylesheet_directory_uri() . '/style.css',
             array('parent-theme-style')
         );
     }
     ```

3. **Activate Child Theme**
   - Go to Appearance → Themes
   - Find your child theme and click "Activate"

## Step 4: Modify Theme CSS

1. **Using Additional CSS Editor**
   - Go to Appearance → Customize → Additional CSS
   - Add custom CSS rules, for example:
     ```css
     /* Change heading color */
     h1, h2, h3 {
         color: #3a86ff;
     }
     
     /* Add custom button style */
     .custom-button {
         background: #ff006e;
         padding: 12px 24px;
         border-radius: 30px;
         color: white;
         text-transform: uppercase;
     }
     
     /* Adjust content width */
     .site-content {
         max-width: 1200px;
     }
     ```
   - Click "Publish" to save changes

2. **Alternative: Edit Child Theme CSS**
   - Add your CSS rules to the child theme's `style.css` file
   - Changes will appear after saving the file

## Step 5: Create a Custom Page Template

1. **Create Template File**
   - In your child theme folder, create a new file named `template-custom.php`
   - Add this code:
     ```php
     <?php
     /**
      * Template Name: Custom Page Template
      * Description: A custom page template for my practical
      */
     
     get_header();
     ?>
     
     <div class="custom-template-container">
         <header class="custom-template-header">
             <h1><?php the_title(); ?></h1>
         </header>
         
         <div class="custom-template-content">
             <?php
             // Start the loop
             while (have_posts()) : the_post();
                 the_content();
             endwhile;
             ?>
         </div>
         
         <aside class="custom-template-sidebar">
             <?php dynamic_sidebar('custom-template-sidebar'); ?>
         </aside>
     </div>
     
     <?php get_footer(); ?>
     ```

2. **Add Custom Styles**
   - Add corresponding CSS to your child theme's `style.css`:
     ```css
     /* Custom Template Styles */
     .custom-template-container {
         display: grid;
         grid-template-columns: 70% 30%;
         gap: 30px;
         max-width: 1200px;
         margin: 0 auto;
         padding: 40px 20px;
     }
     
     .custom-template-header {
         grid-column: 1 / -1;
         text-align: center;
         margin-bottom: 40px;
     }
     
     .custom-template-header h1 {
         color: #ff006e;
         font-size: 3rem;
     }
     ```

3. **Register Sidebar (Optional)**
   - Add to `functions.php`:
     ```php
     // Register custom sidebar
     add_action('widgets_init', 'register_custom_sidebar');
     function register_custom_sidebar() {
         register_sidebar(array(
             'name'          => 'Custom Template Sidebar',
             'id'            => 'custom-template-sidebar',
             'description'   => 'Widgets in this area will be shown on custom template pages.',
             'before_widget' => '<section class="widget %2$s">',
             'after_widget'  => '</section>',
             'before_title'  => '<h2 class="widget-title">',
             'after_title'   => '</h2>',
         ));
     }
     ```

4. **Use the Template**
   - Create or edit a page in WordPress
   - In the Page Attributes section (right sidebar), select "Custom Page Template" from the Template dropdown
   - Publish/update the page

## Verification Steps

1. **Verify Theme Customizations**
   - View your site to see color, font, and layout changes

2. **Verify Child Theme**
   - Check that the child theme is active
   - Make a change to child theme CSS to confirm it overrides parent

3. **Verify Custom Template**
   - Visit the page using your custom template
   - Confirm the layout matches your design
   - Check that the sidebar appears (if added)

## Troubleshooting

If something doesn't work:
1. Check for PHP errors in debug.log
2. Ensure all files are in correct locations
3. Verify file permissions
4. Clear cache if using a caching plugin

This completes the practical assignment for installing and customizing a WordPress theme, creating a child theme, and developing a custom page template.





# WordPress Practical: Plugin Installation and Custom Plugin Creation

## Step 1: Setting Up the Environment (XAMPP)

1. **Install XAMPP** (if not already installed)
2. **Start Apache and MySQL services** from the XAMPP control panel
3. **Place your WordPress files** in the `htdocs` folder (typically `C:\xampp\htdocs\your-site`)

## Step 2: Essential Plugin Installation

### Yoast SEO (SEO Plugin)
1. Download Yoast SEO plugin zip file
2. In WordPress admin:
   - Go to Plugins → Add New → Upload Plugin
   - Upload the Yoast SEO zip file
   - Click "Install Now"
   - Activate the plugin
3. After activation:
   - Go to SEO → Configuration Wizard
   - Follow the setup wizard to configure basic SEO settings

### Wordfence (Security Plugin)
1. Download Wordfence zip file
2. In WordPress admin:
   - Plugins → Add New → Upload Plugin
   - Upload Wordfence zip file
   - Install and activate
3. After activation:
   - Go to Wordfence → Dashboard
   - Click "Start Tour" for initial setup
   - Configure firewall and scan settings

### W3 Total Cache (Caching Plugin)
1. Download W3 Total Cache zip file
2. In WordPress admin:
   - Plugins → Add New → Upload Plugin
   - Upload W3 Total Cache zip file
   - Install and activate
3. Basic configuration:
   - Go to Performance → General Settings
   - Enable Page Cache and Browser Cache
   - Save all settings

## Step 3: Contact Form Plugin (Contact Form 7)

1. Download Contact Form 7 zip file
2. Install and activate like previous plugins
3. After activation:
   - Go to Contact → Add New
   - Create a simple contact form with:
     - Name (text field)
     - Email (email field)
     - Message (textarea)
     - Submit button
4. Copy the shortcode and add it to a page

## Step 4: Image Gallery Plugin (NextGEN Gallery)

1. Download NextGEN Gallery zip file
2. Install and activate
3. After activation:
   - Go to Gallery → Add Gallery/Images
   - Upload some sample images
   - Create a new gallery
   - Add the gallery to a page using the provided shortcode

## Step 5: Social Media Integration Plugin

1. Download a social media plugin (like "Social Media Share Buttons & Social Sharing Icons")
2. Install and activate
3. Configure:
   - Select which social networks to include
   - Choose display locations (posts, pages, etc.)
   - Customize button styles

## Step 6: Creating a Simple Custom Plugin

1. Create a new folder in `/wp-content/plugins/` called `my-custom-plugin`
2. Create a file named `my-custom-plugin.php` inside this folder with this content:

```php
<?php
/*
Plugin Name: My Custom Plugin
Description: A simple custom plugin for college practical
Version: 1.0
Author: Your Name
*/

// Add a simple shortcode to display a message
function my_custom_shortcode() {
    return '<div class="my-custom-message"><p>This content is from my custom plugin!</p></div>';
}
add_shortcode('my_custom_message', 'my_custom_shortcode');

// Add a simple widget
class My_Custom_Widget extends WP_Widget {
    public function __construct() {
        parent::__construct(
            'my_custom_widget',
            'My Custom Widget',
            array('description' => 'A simple custom widget')
        );
    }

    public function widget($args, $instance) {
        echo $args['before_widget'];
        echo $args['before_title'] . 'My Custom Widget' . $args['after_title'];
        echo '<p>This is content from my custom widget!</p>';
        echo $args['after_widget'];
    }
}

function register_my_custom_widget() {
    register_widget('My_Custom_Widget');
}
add_action('widgets_init', 'register_my_custom_widget');

// Add a simple admin notice
function my_custom_admin_notice() {
    echo '<div class="notice notice-success"><p>My Custom Plugin is active!</p></div>';
}
add_action('admin_notices', 'my_custom_admin_notice');
```

3. Go to WordPress admin → Plugins
4. Find "My Custom Plugin" in the list and activate it
5. Test the plugin:
   - Add the shortcode `[my_custom_message]` to a page
   - Go to Appearance → Widgets and add "My Custom Widget" to a widget area
   - Check for the admin notice in the dashboard

## Verification Steps

1. Verify all plugins are active and functioning:
   - Check for Yoast SEO meta boxes when editing posts
   - Verify Wordfence is running scans
   - Check if W3 Total Cache is creating cache files
   - Test the contact form submission
   - View the gallery on a page
   - See social media buttons on posts
   - Confirm custom plugin shortcode and widget work

## Troubleshooting

If any plugins don't work:
1. Check for error messages
2. Verify PHP version compatibility
3. Check that all required files were properly uploaded
4. Try deactivating other plugins to check for conflicts

This completes the practical assignment for installing essential WordPress plugins and creating a custom plugin in an offline XAMPP environment.


