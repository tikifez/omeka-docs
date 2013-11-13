Privilege Assertion
===

Omeka is built off the Zend Framework, so access is controlled largely through the standard Zend methods.

1. Roles, Resources, and Actions are defined
2. Privileges are granted with inheritance plus additional logic to allow or deny
3. Conditional privileges are granted via Assertions

Access Control List
---

The access control list belongs in the _helpers_ folder of your plugin.

* **Example/** (folder)
	* **helpers/** (folder)
		* _Acl.php_

Your ACL class should be named `[PluginName]Acl` and contain a `defineAcl()` method accepting `$acl` as an argument.

### Granting or Denying Access

In most cases you'll define your rules using either <code>[allow()][allow()]</code> or <code>[deny()][deny()]</code>, both of which take arguments of:

1. **Roles** to apply to
2. **Resource** to apply to
3. **Action** to allow or deny
4. **Assertion**, which is a callback which approves or denies the rule by returning a boolean after checking conditional logic

All of the arguments can be given either as a string with the name of the item or, to apply to multiple items, as an array of strings, e.g. `$acl->deny(array('contributor', 'researcher'), 'Items', 'showNotPublic' )`.

**Acl.php**

```php
class LimitedContributorAcl {

	function defineAcl($acl){


		/////////////////////////////
		// Modify Contributor role //
		/////////////////////////////

		$acl->deny(array('contributor', 'researcher'), 'Items', 'showNotPublic' );   
	}
}
```

Useful Functions
---

* [allow()][allow()]
* [deny()][deny()]

[allow()]:  http://omeka.readthedocs.org/en/latest/Reference/libraries/globals/allow
[deny()]:  http://omeka.readthedocs.org/en/latest/Reference/libraries/globals/deny


