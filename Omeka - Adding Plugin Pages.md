Adding a plugin page to Omeka
===

**Important! Remember to follow the Omeka naming conventions outlined in [Plugin Writing Best Practices](http://omeka.readthedocs.org/en/latest/Tutorials/bestPracticesPlugins.html)!**

### Naming Convention Cheat Sheet
* **Plugin names** should be CamelCase.
* **Constants** are always uppercase, separated by underscores, per Zend coding standards.
* **Hooks and Filters** are lowercase, separated by underscores.
* **Private and Protected methods** are prefixed with an underscore.


Create a Controller
---
The controller controls the actions that the page will do.

### Add a controller

Create a controller for the plugin's pages.

+ **Example/** (folder)
	+ **controllers/** (folder)
		+ _IndexController.php_

**IndexController.php** 

```php
/**
 * The Example index controller class.
 *
 * @package Example
 */
class Example_IndexController 
extends Omeka_Controller_AbstractActionController {

	/**
	 * Plugin index page
	 * @return null
	 */
	public function indexAction() {
	}
}
```

This is the minimum required in the controller to display a page for the plugin. The views still need to be built, as well as any menu items you may desire.

Create the Views
---

### Structure
Omeka has three view categories which are reflected in the required directory view directory structure.

1. admin: The user-facing side
2. public: The public-facing side
3. shared: Both admin and public

You may omit the directory for a category you aren't using.


+ **Example/** (folder)
	+ **views/** (folder)
		+ **admin/** (folder)
		+ **public/** (folder)
		+ **shared/** (folder)

Inside of the category directory, you'll need to create a folder for each page, as well as folders for your assets. 

Asset folders are named as follows:

1. common: Common template files
2. css: Stylesheets for the view
3. javascripts: Javascript files to be included
4. forms: Plugin forms

The example uses an admin page but the steps are the same regardless the view category – only the category folder name changes.

				
### Writing a page

For the below examples we'll assume the views structure is similar to the below.

+ **Example/** (folder)
	+ **views/** (folder)
		+ **admin/** (folder)
			+ **index/** (folder)
				+ _index.php_
			+ **common/** (folder)
				+ _example-nav.php_
			+ **css/** (folder)
				+ _example-styles.php_

Use the <code>[head()][head()]</code> method to make the page look like the rest of Omeka.

**index.php**

```php
<?php
	$page_head = array(
		"title" => "Example Plugin",
		"bodyclass" => "primary",
		"content_class" => "horizontal-nav"
	);
	
	echo head($page_head);
```

Use the <code>[common()][common()]</code> method to call files from the _views/admin/common_ directory.

**index.php**

```php
<?php
	$page_head = array(
		"title" => "Example Plugin",
		"bodyclass" => "primary",
		"content_class" => "horizontal-nav"
	);
	
	echo head($page_head);
	echo common("example-nav");
```

Use the <code>[foot()][foot()]</code> method to call the site footer

**index.php**

```php
<?php
	$page_head = array(
		"title" => "Example Plugin",
		"bodyclass" => "primary",
		"content_class" => "horizontal-nav"
	);
	
	echo head($page_head);
	echo common("example-nav");
?>

<p>My plugin's going to be the very best! Like no plugin ever was!</p>

<?php
	echo foot();
?>
```

### Calling a page besides index
Build your logic for redirecting the page* and redirect using  `$this->_helper->redirector->goto('page-name');`

<small>*I realize this is unsatisfactory. For example: how do you get to /example/anotherPage</small>

### Calling a form in your page
<small>Coming soon.</small>

As with other plugin features, forms are stored in their own directory within the plugin and are called from your individual page, facilitating reuse.

* Example/ (folder)
	* forms/ (folder)
		* _MyForm.php_

#### Building form elements
<small>Coming soon…</small>

Form elements are built within the forms directory within a class extending `Omeka_Form`.

**MyForm.php**

```php
class CsvImport_Form_Main extends Omeka_Form
{
    private $_columnDelimiter;
    private $_fileDelimiter;
    private $_tagDelimiter;
    private $_elementDelimiter;
    private $_fileDestinationDir;
    private $_maxFileSize;

    /**
     * Initialize the form.
     */
```



#### Calling form elements
<small>Coming soon…</small>

### Notes
If your common can't find the requested file Omeka will simply throw a 404 rather than showing your page.

Remember to have your text filtered by using `__('Text goes here')`

### Remaining Questions

* How to call a file from the _javascripts/_ path? Or are they automatically added?
* Is there an existing friendly source for information about view functions?


Add Menu Items <small>(optional)</small>
---

### Add an admin menu item

In your Example/ExamplePlugin.php file add a filter to modify the admin navigation menu.

+ **Example/** (folder)
	+ _ExamplePlugin.php_

**ExamplePlugin.php**

```php
/**
 * Add an item to the admin menu
 * @param array $tabs Tabs, <LABEL> => <URI> pairs.
 * @return array The tab array with the "Neatline" tab.
 */
public function filterAdminNavigationMain($tabs){
	$user = current_user();
	$tabs[] = array(
		'label'   => __("Limited Contributor"),
		'uri'     => url('/users/edit/'.$user->id),
		'visible' => true
		);

	return $tabs;
}
```

## Add an admin footer item

**ExamplePlugin.php**

```php
	/**
	 * Add an item to the admin footer
	 * @param  object $request Page request
	 * @return null
	 */
	public function hookAdminFooter($request)
	{
		echo '<h5>This plugin brought to you by developers.</h5>';
	}
```

### Useful Functions

[head()][head()] 
: Gets the common page header, but allowing per-page customization

[foot()][foot()]
: Gets the common page footer, but allowing per-page customization

[common()][common()]
: Gets a common file

[flash()][flash()]
: ?

[html_escape()][html_escape()]
: ?

[head()]: http://omeka.readthedocs.org/en/latest/Reference/libraries/globals/head)
[foot()]: http://omeka.readthedocs.org/en/latest/Reference/libraries/globals/foot
[common()]: http://omeka.readthedocs.org/en/latest/Reference/libraries/globals/common
[flash()]: http://omeka.readthedocs.org/en/latest/Reference/libraries/globals/flash.htm
[html_escape()]: http://omeka.org/codex/Functions/html_escape
