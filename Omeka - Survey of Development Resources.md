Omeka Reference
===

There have been many changes between Omeka 1.x and 2.x. Many of these changes have been documented on the Omeka [Updating Plugins for 2.0](http://omeka.org/codex/Updating_Plugins_For_2.0) page. Some of the links I've found most useful are below.

* Omeka official list of [function replacements][1]


Roles in brief
---

### Standard Omeka (SO) Roles

* super
* admin
* researcher
* contributor


### Adding new roles

Roles are controlled via Zend's [ACL methods](http://framework.zend.com/manual/1.12/en/zend.acl.html). The three methods most likely desired for creating new roles are:

Zend_Acl::addRole

1. Role (string)
2. Role to inherit from (string)

Zend_Acl::allow and Zend_Acl::deny
Assigning any of these a null value makes it apply to all types in that parameter.

1. Zend_Acl_Role_Interface|string|array $roles
2. Zend_Acl_Resource_Interface|string|array $resources
3. string|array $privileges
4. Zend_Acl_Assert_Interface $assert

As an example, to deny the collaborator role from opening items, you could do _$acl->deny('Collaborator', 'Items', 'show');_ which would deny the collaborator role access to the _admin/items/show_ path, denying access to viewing. More is happening than that, of course, but that's the most visible side of it.


Omeka Resources in Brief
---

### Standard Omeka (SO) resources:

#### Nodes

* Items
* Collections
* ElementSets
* Files
* Plugins

#### Settings

* Settings
* Security
* Upgrade
* Tags
* Themes

#### Administrative

* SystemInfo
* ItemTypes
* Users
* Search
* Appearance


### Adding new resources

TBD



Omeka Permissions in Brief
---

### Abstract actions

index
: Forwards to browse action.

browse
: Retrieve and render a set of records for the controller's model.

show
: Retrieve a single record and render it.

add
: Add an instance of a record to the database

edit
: Similar to the 'add' action, except this requires a pre-existing record.

delete-confirm
: Ask for user confirmation before deleting a record.

delete
: Delete a record from the database.


### Account actions

activate
: Activate user.

confirm
: Sends account confirmation email to user email.

login
: Login user.

logout
: Logout user.

me 
: Redirects to user home

forgot-password
: Lost password

register
: Registers a user account.

staleToken
: ?

updateAccount
: Updates Account Action



### Item actions

add
: ?

batchEdit
: Allows user to make batch changes to files, such as deleting

batchEditSave
: ?

browse
: ?

changeType
: ?

edit
: ?

editSelf
: ?

editAll

deleteSelf

deleteAll

makeFeatured

makePublic

modifyPerPage

pagination
: ?

showNotPublic

showSelfNotPublic

search
: ?

tags
: ?

untagOthers
    


### Item type actions

add
: ?

addExistingElement
: ?

addNewElement
: ?

changeExistingElement
: ?

edit
: ?


### Plugin actions

activate
: ?

add
: ?

browse
: ?

config
: ?

deactive
: ?

delete
: ?

install
: ?

uninstall
: ?

upgrade
: ?


### Settings actions

index
: ?

browse
: ?

editSecurity
: ?

editSettings
: ?

editSearch
: ?

editItemTypeElements
: ?

checkImageMagick
: ?

getFileExtensionWhitelist
: ?

getFileMimeTypeWhitelistAction
: ?

getHtmlPurifierAllowedHtmlElements
: ?

getHtmlPurifierAllowedHtmlAttributes
: ?


### Action you probably don't need to know about

autocomplete
: ?

config
: ?

editNavigation
: ?

editSettings
: ?

elementForm
: ?

error
: ?

forbidden
: ?

methodNotAllowed
: ?

migrate
: ?

notFound
: ?

rename
: ?

switch
: ?






### General

add
: Add an item

addSection
: ?

browse
: ?

delete
: Delete an item

delete-confirm
: ?

deleteSection
: ?

deleteSelf
: ?

edit
: Edit an item

editSection
: ?

editSelf
: Editing a resource owned by the current user.

editorSelf
: ?

importSelf
: ?

index
: ?

putSelf
: ?

show
: See a resource. For items this means the non-thumbnail view.

showNotPublic
: See a resource which isn't public

showSelfNotPublic
: Showing a resource owned by the current user which isn't public

tag
: Tag items


Specific tasks
===

Hiding items from browse
---

John Flatness of the Omeka Dev Team suggests making a plugin to hide a particular item type or collection from browse. [Exhibit not displaying non-public items](http://omeka.org/forums/topic/exhibit-not-displaying-non-public-items)

Bibliography
===

1. "Updating Plugins for 2.0 - Codex - Omeka." § Function Replacements Accessed July 30, 2013. [http://omeka.org/codex/Updating_Plugins_For_2.0#Function_Replacements][1]



[1]: http://omeka.org/codex/Updating_Plugins_For_2.0#Function_Replacements "Omeka 2.x function replacements"
