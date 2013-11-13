Zend Naming Conventions Cheat Sheet
===

[Word of God Naming Conventions](http://framework.zend.com/manual/1.12/en/coding-standard.naming-conventions.html#coding-standard.naming-conventions.functions-and-methods)

Classes
---

* Zend_Db_Table: Acceptable. Maps to "Zend/Db/Table.php".
* Zend_Pdf: Acceptable.
* Zend_pdf: Unacceptable. Each word needs to start with a majuscule letter followed by all minuscule letters.
* Zend_PDF: Unacceptable. Each word needs to start with a majuscule letter followed by all minuscule letters.
* Zend_Db_Table2: Tolerated but discouraged. Classes are strongly encouraged to avoid numbers.
* Zend_Not_From_Zend_Library: Unacceptable. Only classes the Zend framework nor related libraries should start with "Zend"


Abstract Classes
---

* Zend_Controller_PluginAbstract: Acceptable.
* Zend_Controller_Plugin_PluginAbstract: Acceptable.
* Zend_Controller_Plugin_Abstract: Unacceptable. There cannot be an underscore before the suffix "Abstract" due to namespace usage.


Interfaces
---

* Zend_Controller_PluginInterface: Acceptable.
* Zend_Controller_Plugin_PluginInterface: Acceptable.
* Zend_Controller_Plugin_Interface: Unacceptable. There cannot be an underscore before the suffix "Interface" due to namespace usage.


Filenames
---

* MyFile.php: Acceptable.
* MyFile-v2-3-4: Acceptable.
* My-file.php: Acceptable.
* My_file.php: Acceptable.
* MyFile.xyz: Conditionally Acceptable. Files containing PHP code require an extension of _php_
* My File.php: Unacceptable. Spaces are not permitted.


Functions and Methods
---

* filterInput(): Acceptable. Descriptive verbosity is encouraged.
* WidgetFactory(): Unacceptable. Functions and methods must start with a minuscule letter.
* widgetfactory(): Unacceptable. Functions and methods should be camelcase.
* widget_Factory(): Unacceptable. Underscores are not allowed.
* widgetFactory2(): Tolerated but discouraged. Functions and methods are strongly encouraged to avoid numbers.
* getElementById(): Acceptable.
* fetchElementById(): Unacceptable. Accessors for instance or static variables should start with _get_ or _set_.
* _privateMethod(): Acceptable.
* _protectedMethod(): Acceptable.
* _publicMethod(): Unacceptable. Only private and protected methods should start with an underscore.
* _filterInput(): Unacceptable. Only private and protected methods should start with an underscore.


Variables
---

* $userId: Acceptable.
* $user_id: Unacceptable. Must be alphanumeric.
* $Userid: Unacceptable. Must start with minuscule letter and be camelcase.
* $i: Conditinally acceptable. Indescriptive so should be used for only the smallest loops.


Constants
---

Only acceptable as class members with the _const_ modifier -- not globally with the _define_.


* EMBED_SUPPRESS_EMBED_EXCEPTION: Acceptable.
* Embed_Suppress_Embed_Exception: Unacceptable. Must be all caps with words separated by underscores.
* EMBED-SUPPRESS-EMBED-EXCEPTION: Unacceptable. May only be alphanumeric with underscores.
* EMBED_SUPPRESSEMBEDEXCEPTION: Unacceptable. Words must be separated by underscores.



Zend Acl Cheat Sheet
===

Zend's ACL is managed through creation of _roles_ which request access to _resources_.


Roles
---

_Roles_ are objects which request access.

_Zend_Acl::addRole_

1. Role (string)
2. Role to inherit from (string)

TBD



Resources
---

_Resources_ which are objects to which the permission set will be applied, e.g. a specific page.

TBD


Defining Permissions
---

_Zend_Acl::allow_ and _Zend_Acl::deny_
Assigning any of these a null value makes it apply to all types in that parameter.

1. `Zend_Acl_Role_Interface` |string|array $roles
2. `Zend_Acl_Resource_Interface` |string|array $resources
3. string|array $privileges
4. `Zend_Acl_Assert_Interface` $assert


Conditional Permissions through Assertions
---

Conditional permissions are handled by _assertions_ -- classes implementing the _assert()_ method.

```php
class CleanIPAssertion implements Zend_Acl_Assert_Interface {
	public function assert( Zend_Acl $acl, Zend_Acl_Role_Interface $role = null, $resource = null, $privilege = null) {
		return $this->_isCleanIP($_SERVER['REMOTE_ADDR']);
	}
	
	protected function _isCleanIP($ip) {
		// …
	}
}
```

The assertion may then be called by a defined rule. Permission will only be granted if the assertion returns true.

```php
$acl = new Zend_Acl();
$acl->allow(null, null, null, new CleanIPAssertion());
```

For more in-depth explanation with the nuances, see the Zend ACL [Advanced Usage](http://framework.zend.com/manual/1.12/en/zend.acl.advanced.html) page.


