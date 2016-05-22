# ServletActionFramework
This is a maven project written in Java.  It adds action classes to old Servlet/JSP based apps.


Features
========

- Handle each load and submit events with dedicated action classes.
- Automatic injection and type conversion of form parameters to action fields.
- Simplified JSP page forwarding and redirection.


Required Dependencies
=====================

- `javax.ejb`.  For injecting `EJB` from `Servlet` to `Action` class.
- `javax.servlet`


Basic use
------------
**How do you define a servlet?**
Define a Servlet by annotating with `@WebServlet` like you normally do, but subclass `ph.rye.saf.SafServlet`.

**How do you define a Load action?**

1.  Subclass `ph.rye.saf.BaseAction`.
2.  Annotate your servlet class with `@RequestAction` and pass the class of the `BaseAction` subclass.
3.  Implement `accept()` method to handle specific event or return `true` to run in any circumstance.
4.  Put loading code inside `execute()` method.

**How do you define a Load action?**

1. Subclass `ph.rye.saf.BaseAction`.
2. Annotate your servlet class with `@SubmitAction` and pass the class of the `BaseAction` subclass.
3. implement `accept()` method to handle specific event or return `true` to run in any post event.
4. Put submit handler code inside `execute()` method.


**How do you make the page form recognizable by `SAF`?**

Page must set a form value with the name event to the name of the button that initiated the submit.
Example code with `jQuery`.
```javascript
  /* Handle form submission, prevent submit if button is disabled, set event
	   property to the name of the button on submit. */
	$("form").submit(function(event) { 
        var button = $("button[clicked=true]");
        if (button.hasClass('disabled')) {
            return false;        	
        } else {
            $("input[name='event']").val(button.attr("name"));
		}
   	});
   	
	$("form button").click(function() {
	    $("button", $(this).parents("form")).removeAttr("clicked");
	    $(this).attr("clicked", "true");
	});
```



