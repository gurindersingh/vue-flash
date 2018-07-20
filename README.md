# @gurinder/vue-flash

### Usage

```php
// Add Flash level to master
@php
	
	$flashLevel = session('error') ? 'error' : 'success';
	$flashLevel = session('warning') ? 'warning' : $flashLevel;
	$flashLevel = session('info') ? 'info' : $flashLevel;

	$flashMessage = session('error') ? session('error') : session('success');
	$flashMessage = session('warning') ? session('warning') : $flashMessage;
	$flashMessage = session('info') ? session('info') : $flashMessage;

@endphp
```

```js
// Dependancy
import Event from '@gurinder/vue-eventy';
window.Event = new Event();

// Register Flash
import flash from '@gurnder-vue-flash';
Vue.component('vue-flash', flash);
window.flash = (message, level = 'success', timeout = 3000) => window.Event.fire('flash', {message, level, timeout});

<vue-flash data-level="success" data-message="message"></vue-flash>

```