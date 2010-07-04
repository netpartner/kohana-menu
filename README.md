# Menu generator for Kohana 3

## Basics

The menus are defined in configuration files, which must be placed in the "config/menu" folder.

See [config/menu/default.php](http://github.com/b263/kohana-menu/blob/master/config/menu/default.php)

To render the menu without modifications, call:

	Menu::factory()->render();

## Config files

You can use different config files, by setting the factory method's $config parameter.

### Example: Load menu configuration based on user role

	$menu = Menu::factory($role); // this could use `config/menu/(user|admin).php`

## Marking the current menu item

The config setting `current_class` defines the css class, which will be used by the `set_current()` method, to mark the current menu item:

	$menu->set_current('artice/show');

The parameter of `set_current()` is the URL segment of the respective item.

## Changing menu item settings

You can change the settings of each item with the following methods:

	$item_url = 'home';
	$menu->set_title($item_url, 'New title')
		 ->add_class($item_url, 'active')
		 ->remove_class($item_url, 'inactive')
		 ->set_url($item_url, 'new/url');

## Matching URLs

By default, the URL parameter must exactly match the predifined `url` setting of the menu item, which could have changed in the meantime, by a call of `set_url`:

	$menu->set_url('artice/show', 'article/show/123');

You can change this behaviour with the static `$str_comp_mode` property:

	Menu::$str_comp_mode = Menu::STR_COMP_MODE_CONTAINS; // uses strstr(), no regex support
	// default value is Menu::STR_COMP_MODE_EXACT