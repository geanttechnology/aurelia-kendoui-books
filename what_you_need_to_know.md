# What you need to know
There are a few things you should know when working with the aurelia-kendoui-bridge.
<br>
<br>
#### Conventions
Just like Aurelia, we use conventions. All custom elements and custom attributes use the `ak-` prefix, all properties are prefixed with `k-` and all events use the `k-on-` prefix.

For example, the [kendo API documentation](http://docs.telerik.com/kendo-ui/api/javascript/ui/button#configuration-enable) of the Button control, mentions an `enable` property.

This translates into this HTML tag:

    <input ak-button="k-enable.bind: true"/>

Here we are using the `ak-` prefix for the button custom attribute and the `k-` prefix for the `enable` property of the button.
<br><br>

It is also possible to delegate Kendo events. The `k-on-` prefix has to be used here.

To illustrate this, we'll take a look at the [open](http://docs.telerik.com/kendo-ui/api/javascript/ui/autocomplete#events-open) event of the Autocomplete control. This translates into:
<br><br>

    <ak-autocomplete k-data-source.bind="items" k-on-open.delegate="myFunction($event.detail)">
      <input style="width: 100%;">
    </ak-autocomplete>
    
<br><br>

Notice the `k-on-` prefix for the autocomplete custom element and the `k-on-` prefix for the `open` event of the autocomplete control. The $event's detail property contains the original event raised by the Kendo control. In order to pass this to the `myFunction` function directly, we use `$event.detail` in the view directly.
<br>
<br>
#### Binding
Using Aurelia's `.bind` syntax on a property allows it to do two things: binding to a variable and type parsing.
<br>

If you would use `k-visible="true"` without `.bind`, the `k-visible` property will contain the value of "true" (as string, not as boolean).
<br>

By adding `.bind` after the property name, it is parsed by Aurelia's binding syntax as a boolean, which is what we need. `k-visible.bind="true"` is the correct syntax. So for integers, strings and objects, and function calls use `.bind`.
<br><br>

A couple of examples:

	k-title="my string title"
	k-visible.bind="true"
	k-max-integer-value.bind="15"
	k-type.bind="{ name: 'a' }"
	k-title.bind="aPropertyOnMyViewModel"
    k-mask.bind="getMask()"
	k-my-array-value.bind="['a', 'b']"
<br>
<br>
### How to get to the Kendo control
Every wrapper exports a `k-widget` property that you can two-way bind to.

      <ak-autocomplete k-data-source.bind="items" k-widget.bind="autocomplete">
        <input style="width: 100%;">
      </ak-autocomplete>
<br><br>

You can then use the `autocomplete` variable to communicate with the Kendo widget.

**IMPORTANT**: **the binding system has not finished in `attached()` causing the bound variable (`autocomplete` in the sample above) to be undefined. If you need to communicate with the widget from inside the `attached` or `bind` callback, use either the `view-model.ref` approach or use the taskque (sample below).**
<br><br>

#### Taskqueue
	import {TaskQueue, inject} from 'aurelia-framework';

	@inject(TaskQueue)
	export class Sample {
		constructor(taskQueue) {
			this.taskQueue = taskQueue;
		}

		attached() {
			this.taskQueue.queueTask(() => {
			  this.autocomplete.enable(false);
			});
		}
	}
    
**(We have made a `@delayed` decorator to make this easier. Check out [this sample](http://aurelia-ui-toolkits.github.io/demo-kendo/#/samples/generic/use-widget-on-initialization))**
<br>
<br>
