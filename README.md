# DataTables-ColumnSearching
Add search controls for columns in the header or footer of the table

##Options
* `placement` - String: "head' or "foot" (default "head")
* `select` - Array of objects: define which columns should search via drop down.  Object properties specified below.

    * `name` - int or string: column index, `columns.data` as a string
    
    * `options` - **Array of Strings**:
     				The string array can specify the value and text of the option by using a `|` 
                    in the String "avalue|Text To Display".  
                    The plugin will assign the String to the value and text of the option if the pipe is omitted.
     				
     				**or a function** function(select){ }  
    				The function will be responsible for appending the `<option/>` elements to the select passed in.  
    				The select it a jQuery object.  
    				
    				
    * `header` - boolean: True to generate an option header in the select.  (default true)
 * `placeholders` - boolean: True generates a placeholder attribute on the inputs using the column header in the table.
 * `controlClass` - String: Classes to apply to the controls.  (default "form-control" for Bootstrap)

Plugin can be invoked by doing:
```js
var dt = $("#mytable").DataTable();
//using defaults
new $.fn.dataTable.DtColSearch(dt);


//OR specify some options
new $.fn.dataTable.DtColSearch(dt, {
	placement: "foot",
	placeholders: "false",
	select: [
		{
			name: "myDataProp",
			
			options: ["1|One", "2|Two", "3|Three"]
		},
		
		{
			name: "anotherSelect",
			
			options: function(jqSelect) {
				var opt1 = $("<option/>").val("1").text("One");
				var opt2 = $("<option/>").val("2").text("Two");
				var opt3 = $("<option/>").val("3").text("Three");
				
				jqSelect.append(opt1, opt2, opt3);
			}
		}
	]
});
```

##Responsive Integration
A special event needed to be added to the Responsive plugin for proper integration.  This change is waiting
approval into the master DataTables/Responsive repo.  In the mean time, you can grab a modified copy from [here](https://github.com/zepernick/Responsive/tree/resize-event)

##JSFiddle Example
[DataTables-ColumnSearching in action](http://jsfiddle.net/zepernick/s7xmz7g3/)