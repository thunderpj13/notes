# golang
------------------------
**BASIC**
-----------------
> 1. if initializing value, ignore type, if declare, ignore var.
> 2. no automatic type conversion.
> 3. typed constant: const a int = 5
> untyped constant: const a = 5
> 4. named return value:
> 		act as being declared  in the first line of the function,
> 		and automatically returned.
> 5.	blank identifier:
> 		_ can be used in place of any vlaue of any type. discard
> 6.	exported names started with capitalized character.
> 7. the order of package initialization:
> >		1.  package variables 
> >		2.  init() (no parameter, no return value)
>
> 8.   if statement; condition {  
>       } else {
>       } 
>
> 9. 	for initialisation; condition; post {  
> 	}       optionlal argument
> 	for {  
> }	infinite loop
> 	
> 10. array:	
> 		a := [...]int{12, 78, 50}
> 		for _, v := range a
>
> 	```golang
> 	c := []int{6, 7, 8} //c is a slice reference
> 	c := [...]int{6, 7, 8} //c is of type int[3]
> 	```
> 	
> 11. slice:
> 	
> 	​	len(slice): 
> >	the number of elements in the slice
>
> 		cap(slice): 
> >	the number of elements in the underlying array 
> >	starting from the index from which the slice is created.
>
> 		func make([]T, len, cap) []T:
> >	can be used to create a slice by passing the type, length and capacity.
> >	The capacity parameter is optional and defaults to the length. The make function creates an 
> >	array and returns a slice reference to it.
>
> 	func append(s []T, x...T) []T:
> >	when new elements are appended to the slice, a new array is created. The elements of the existing 
> >	array are copied to this new array and a new slice reference for this new array is returned. The capacity 
> >	of the new slice is now twice that of the old slice. 				
>
> 12. map										     *
> 	make(map[type of key]type of value) 										     *
> 	value, ok := map[key] If ok is true, then the key is present							     *
> 	delete(map, key) is the syntax to delete key from a map								     *
> 	Similar to slices, maps are reference types									     *
> 	maps are not comparable.								     			     *
> 13. rune:	to cope with utf-8 characters that occupies more than one byte.							     *
> 		A rune is a builtin type in Go and it's the alias of int32							     *.
> 		runes := []rune(string)												     *
> 		len(s) is used to find the number of bytes									     *
> 		The RuneCountInString(s string) (n int) function of the utf8 package can be used to find the length of the string    *
> 14. pointer:
> 		var a *int = &b
> 		The new function takes a type as argument and returns a pointer to a newly allocated zero value			     *
> 		The Go compiler is intelligent enough and it will allocate necessary local variable on the heap.
> 15. struct:
> 		The Go language gives us the option to use emp8.firstName instead of the explicit dereference (*emp8).firstName.
> 		Anonymous fields:
> 			structs with fields that contain only a type without the field name.
> 			by default the name of an anonymous field is the name of its type

------------------------------------------
**ADVANCED**
-------------------------------
>1. 	method:
>		func (t Type) methodName(parameter list) {  }     //receiver
>		pointer receiver
>			just use e.changeAge(51). e.changeAge(51) will be interpreted as (&e).changeAge(51) by the language.
>		To define a method on a type, the definition of the receiver type and the definition of the method should be present in the same package.
>		create a type alias for the built-in type int and then create a method with this type alias as the receiver.
>	
>2. 	buffered channel:
>	  	make(chan int, capacity)
>       	 len(chan): number of elements currently in the buffer of the channel
>      	cap(len): capacity
> 
>3. WaitGroup:
>     import "sync"
>     wg.Add(int): the wg's counter is incremented by this parameter.
>    wg.Done(): the counter is decremented.
>    wg.Wait(): block until the counter becomes zero.
>    notice: the wg should passes by pointer.
>
>4. range channel will keep reading until the channel is closed.
>
>5.  select:
>     The select statement blocks until one of the send/receive operation is ready. If multiple operations are ready, one of them is chosen at random.
>     	If a default case is present, this deadlock will not happen since the default case will be executed when no other case is ready. 
>     	empty select {} will block forever.
>
>6. 	 mutex:
>          	in the sync package
>          	mutex.Lock()
>          	mutex.Unlock()
>
>7.  defer:
>     	The arguments of a deferred function are evaluated when the defer statement is executed and not when the actual function call is done.
>     	When a function has multiple defer calls, they are pushed on to a stack and executed in Last In First Out (LIFO) order.
>
>8. error handling:
>    	The idiomatic way of handling errors in Go is to compare the returned error to nil. A nil value indicates that no error has occurred and a non-nil value indicates the presence of an error. 
>      	type error interface {  
>          		 Error() string
>            	}
>
>9. custom error handling:
>
>  ```golang
>  // Package errors implements functions to manipulate errors.
>    	package errors
>  
>    	// New returns an error that formats as the given text.
>    	func New(text string) error {
>   	 return &errorString{text}
>    	}
>  
>   	 // errorString is a trivial implementation of error.
>    	type errorString struct {
>  	  s string
>    	}
>  
>    	func (e *errorString) Error() string {
>    	return e.s
>    	}
>  ```
>
>10. panic and recover:
>       	func panic(interface{})  
>       	func recover() interface{}  
>       	When a function encounters a panic, its execution is stopped, any deferred functions are executed and then the control returns to its caller. This process continues until all the functions of the current goroutine have returned at which point the program prints the panic message, followed by the stack trace and then terminates.
>       	Recover is useful only when called inside deferred functions. 
>11. closure:
>       	Closures are a special case of anonymous functions. Closures are anonymous functions which access the variables defined outside the body of the function. 
>       	Every closure is bound to its own surrounding variable. 
>12. reflect:
>       	The reflect package implements run-time reflection in Go.
>       	reflect.Type
>       	 reflect.Value
>       	reflect.TypeOf() and reflect.ValueOf() which return the reflect.Type and reflect.Value respectively.



-----------------------------------------END----------------------------------------