1. Circular dependency
	1. can you give examples in functional programming like lisp, etc,...
	2. Technical name being dependency resolution issues - meaning this only happens with dependencies like import, etc... ?
2. Factory function
	1. This function is executed lazily by the DI system when the dependency is needed ?
		1. export function forwardRef( - this is the one angular will call to lazily execute the forwardRefFn Factory function like mentioned as "forwardRef.forwardRef"?
		2. forwardRefFn is the factory function, which wraps the reference to the actual dependency: all i see is () => any
3. Only Evaluated When the Dependency is Resolved’
	1. so instead of storing all the forwardRef markers (**Token Resolution**: Angular stores a special “forward reference” marker and later resolves the actual dependency using the provided factory.) in a key-value map (or more efficient data structure). Angular maintainers simply call resolveForwardRef in all the places where any dependency is needed and if the dependency is wrapped with forwardRef then the actual forwardRef function is called or else simply calling the resolution would work ? - is this what this do ?
		1. ```if (isForwardRef(type)) {
				    return type.forwardRef();
				} else {
					return type;
			 }```
4. React’s forwardRef and Deferred Execution - can you deep dive here how parent would get access to child's internal dom nodes only via forwardRef (Imagine a parent wants direct control over a DOM element inside a child. Without forwardRef, the parent would have no access to the child’s internal structure.)?

1. Angular Di
	1. what strong evidence that you have to tell that angular DI is Service Locator Design Pattern. Deep dive. Give me precise code samples(with inline commented detailed explanations for necessary lines) in angular source code.
	2. _Deferred Binding_: Binding is deferred until runtime when all necessary dependencies are available - so here the binding of which entity needs which dependencies is done only at app level (where components, services, pipes, directives in it's constructor mention they need these dependencies (along with decorators like self, optional, etc...) or using inject function)?

Learn NG_VALIDATORS is used (in the context of polymorphic maybe - reiterate this after below polymorphic - ask chatgpt to compare this all implementation of all valueAccessors default, inputValueAccessor, etc... with the polymorphic nature of ngControl) in the context of multi provider (deep dive here). quantum entanglement of dual nature
Search through how ngcontrol is provided with all the other polymorphic resolution with ngmodel, form_control_directive, form_control_name (Learn ngmodel first everything about it with first principles down to the quantum entanglement HA HA..) - This is mainly to learn about how useExisting is needed for providers without the multi.