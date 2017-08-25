# React Specification

## File organization

-[enforce] the same directory must not have '. js ' and '. Jsx ' files with the same name.

When you use module import, you tend to not add suffixes, and if you have files with the same name but different suffixes, the build tool will not be able to determine which one is the module that needs to be introduced.

-[Force] component files use a consistent '. js ' or '. jsx ' suffix.

The suffix name for all component files is chosen either from '. js ' or '. Jsx '.

Some of the components that are '. js ' files should not appear in the project, partly '. Jsx '.

-[Force] Each a file exposes a component in the form of ' export default '.

Allows multiple components to exist in one file, but only one component is allowed to be exposed through ' export default ', and the other components are defined as internal components.

-[force] Each storage component's directory uses an ' index. js ' to expose all components in the form of named exports.

References to components within a directory use ' Import Foo from './foo ';

Components referencing other directories use ' Import {Foo} from ' ... /component ';

Plugins such as [Vscode Export-index plugins] (https://marketplace. Visual Studio. Com/items Itemname=brunolm Export-index) are recommended to automatically generate ' index. js ' content.

## Naming rules

-the [force] component is named Pascalcase.

Includes function components, with names of Pascalcase.

-The Force component name remains the same as the file name.

At the same time the component name should reflect the functionality of the component to determine which component to use by observing the filename.

-[force] higher-order components are named using CamelCase.

The higher-order component is in fact not a component, but a "build component type" function, so follow the specification of the JavaScript function naming, using CamelCase naming.

-[enforce] use the ' onXxx ' form as the name of the property used for the callback in ' props '.

Using a uniform naming convention to differentiate between callbacks and non-callback attributes in ' props ', you can see clearly a component's logical interaction up and down on the JSX.

For properties that are not used for callback functions, use verbs as property names.

' ' JavaScript
OnClick as callback with on, RenderText non-callback function uses verb
Let Label = ({onClick, rendertext}) => <span onclick={onclick}>{rendertext ()} </span>;
```

-[Recommended] Use the word ' withxxx ' or ' xxxable ' as the name of the higher-order component.

Higher-order components are functions that add behavior and functionality to a component, so using the words in the above form helps to understand their functionality.

-the event handler function as a component method is named as a word with business meaning, not in the form of ' onXxx '.

' ' JavaScript
,
Class Form {
@autobind
Collectandsubmitdata () {
Let data = {
Name: this.
Age: the This.
};
this. Props onSubmit (data);
}

@autobind
Syncname () {
// ...
}

@autobind
Syncage () {
// ...
}

Render () {
Return (
<div>
<label> Name: <input = "text" Onchange={this. Syncname}/> </label>
<label> Age: <input = "number" Onchange={this. Syncage}/> </label>
<button = "button" Onclick={this collectandsubmit}> submit </button>
</div>
);
}
}
```

## Component Declarations

-[Force] Use ES class to declare components and prohibit the use of ' react. Createclass '.

[React V15.5.0] (https://facebook. GitHub. Io/react/blog/2017/04/07/react-v15.5.0. html) has deprecated the ' react. Createclass ' function.

' ' JavaScript
Bad
Let message = react. Createclass ({
Render () {
Return to <span> {this. state. message} </span>;
}
});

,
Class Message extends Purecomponent {
Render () {
Return to <span> {this. state. message} </span>;
}
}
```

-the component that [force] does not use ' state ' declares as a function component.

function components have a special place in react and are likely to get more internal optimizations in the future.

' ' JavaScript
Bad
Class Nextnumber {
Render () {
Return <span> {this. props. Value + 1} </span>
}
}

,
Let Nextnumber = ({value}) => <span> {value + 1} </span>;
```

-[Force] all components need to declare ' proptypes '.

' Propstypes ' is a component-like document that facilitates the reading and understanding of code while enhancing component robustness.

-[Force] declares the corresponding value in ' Defaultprops ' for all attributes that are not ' isrequired '.

Declaring an initial value can help you understand the initial state of the component, or reduce the overhead of ' proptypes ' for type validation.

For properties that have no value initially, you should declare that the initial value is ' null ' rather than ' undefined '.

-[force] if not necessary, use static attribute syntax to declare ' propstypes ', ' contexttypes ', ' defaultprops ' and ' state '.

Only when the initial ' state ' needs to be computed from ' props ', will the declaration of ' states ' be placed in the constructor, otherwise the static attribute declaration is used.

-[enforce] arrange the methods and properties in the assembly in the specified order.

The methods and properties in the component are organized in the following order:

1. ' Static DisplayName '
2. ' Static proptypes '
3. ' Static contexttypes '
4. ' State Defaultprops '
5. ' Static state '
6. Other Static properties
7. For event handling and in the manner of attributes (' OnClick = e => {...}} ') Method of declaration
8. Other instance Properties
9. ' Constructor '
' Getchildcontext '
' Componentwillmount '
' Componentdidmount '
' Shouldcomponentupdate '
' Componentwillupdate '
' Componentdidupdate '
' Componentwillunmount '
17. Event Handling Methods
18. Other methods
' Render '

where ' shouldcomponentupdate ' and ' render ' are the most easily readable functions of a component, so it helps to locate them quickly.

-no explicit introduction of react objects is recommended.

Using JSX implicitly relies on the "React" object in the current environment, but is not explicitly used in the source code, which in this case adds ' import react from ' react '; ' will cause an unused variable to exist.

Using the [Babel-plugin-react-require] (https://www. Npmjs. Com/package/babel-plugin-react-require) plug-in can solve this problem well, so it is not necessary to explicitly write ' import react from ' react;

-[Recommended] Use the ARROW function to declare a function component.

The arrow function has a more concise syntax (no ' function ' keyword) and can omit the extra indentation caused by ' return ' when there is only one statement.

-The ' DisplayName ' attribute is added when the [recommended] higher-level component returns a new component type.

At the same time declare the existence of higher-order components on ' displayName '.

``` JavaScript
,
Let aspurecomponent = Component => {
Let componentname = Component. DisplayName | | Component. Name | | ' Unknowncomponent ';
Return class extends Purecomponent {
static DisplayName = ' Aspure (${componentname}) '

Render () {
Return <component {... this. props}/>;
}
};
};
```

## Component Implementation

-[Force] all components are conceptually implemented as pure components (Pure Component), except for the top or routing-level components.

This rule does not require the component to inherit from ' Purecomponent ', ' the concept of pure components ' means that a component in the case of ' props ' and ' state ' does not change (shallowequal), the render result should be consistent, that is ' shouldcomponentupdate ' should return ' false '.

A typical non-pure component is a function that uses a random number or date.

' ' JavaScript
Let Randomnumber = () => <span> {Math. Random ()} </span>;
Let Clock = () => <span> {Date. Time ()} </span>;
```

A typical non-pure component is a function that uses a random number or date.

``` JavaScript
Let Randomnumber = () => <span> {Math. Random ()} </span>;
Let Clock = () => <span> {Date. Time ()} </span>;
```

Non-pure components have an upward "contagious", that is, a component containing impure components must also be a non-pure component, followed by the component tree structure up. Because non-pure components cannot optimize rendering performance through ' shouldcomponentupdate ' and are contagious, avoid being used in a non-top level or routing component.

If you need to use a random number, date, and other impure data on a node in the component tree, you should generate this value from the top-level component and pass it through ' props '. For systems that use state management such as Redux, you can store relevant values in the application state (such as Redux using action Creator to generate these values and update them to the store through action and reducer).

-[force] prohibits writing ' shouldcomponentupdate ' implementations for components inherited from ' purecomponent '.

Reference [react related issue] (https://github. com/facebook/react/issues/9239), in react implementations, ' purecomponent ' does not directly implement ' shouldcomponentupdate ', but adds a ' isreactpurecomponent ' tag, by ' Compositecomponent ' realizes the relevant logic by identifying this tag. So customizing ' shouldcomponentupdate ' on ' purecomponent ' and not enjoying the logical reuse of ' super. Shouldcomponentupdate ' also makes this inheritance relationship meaningless.

-[enforce] implement the ' shouldcomponentupdate ' method for pure components that are not inherited from ' purecomponent '.

The ' shouldcomponentupdate ' approach plays a crucial role in the performance of react the pure component must be able to decide whether to render by the ' props ' and ' state ', so if the component is a pure component and does not inherit ' shouldcomponentupdate ', it should have its own ' shouldcomponentupdate ' implementation to reduce unnecessary rendering.

-[Recommended] add ' purecomponent ' capabilities to function components.

The function component is not necessarily a pure component, so its ' shouldcomponentupdate ' implementation is ' return true; ', which can lead to additional meaningless rendering, so it is recommended to use higher-order components to add ' shouldcomponentupdate ' logic to it.

It is recommended that you implement this functionality using the [react-pure-stateless-component] (https://www. Npmjs. com/package/react-pure-stateless-component) Library.

-[Recommended] use ' @autobind ' for event-handling methods to bind to ' this '.

Because ' purecomponent ' uses [' shallowequal '] (https://github. com/facebook/fbjs/blob/master/packages/fbjs/src/core/shallowequal. js) ' To render judgment if you use ' bind ' or arrow function bindings ' This ' in JSX The function that causes the subassembly to get every time is a new reference, this destroys the logic of ' shouldcomponentupdate ' and introduces meaningless repetitive rendering, so you need to bind the event handling method to ' this ' before the ' render ' call and get the same reference in every ' render ' call.

The current more popular method of binding ' This ' is 2, one of which uses the syntax of the class attribute:

``` JavaScript
Class Foo {
OnClick = e => {
// ...
}
};
```

The second use of ' @autobind ' adorners:

``` JavaScript
Class Foo {
@autobind
OnClick (e) {
// ...
}
}
```

Using class attribute syntax, although you can avoid introducing a ' autobind ' implementation, there are some drawbacks:

1. It is not easy for beginners to understand the definition of ' this ' within a function.
2. The function cannot be used in other adorners (such as ' memoize ', ' deprecated ' or inspection-related logic, etc.).

Therefore, it is recommended that the ' @autobind ' adorner be used to implement the prior binding of ' this ', and the associated adorner implementation provided by the [Core-decorators] (https://www. Npmjs. Com/package/core-decorators) library is recommended.

## JSX

-[Force] non-dom components that do not have child nodes use the self-closing syntax.

For DOM nodes, closed in accordance with the relevant rules of the HTML encoding specification, * where void element uses the self-closing syntax * *.

``` JavaScript
Bad
<Foo> </Foo>

,
<foo/>
```

-[force] keeps the start and end tags indented at the same level.

For other statements in front of the label, such as ' return ', use parentheses for line breaks and indents.

``` JavaScript
Bad
Class Message {
Render () {
Return <div>
<span> Hello World </span>
</div>;
}
}

,
Class Message {
Render () {
Return (
<div>
<span> Hello World </span>
</div>;
);
}
}
```

For direct ' return ' function components, you can use parentheses without the curly braces and the ' return ' keyword:

``` JavaScript
Let message = () => (
<div>
<span> Hello World </span>
</div>
);
```

-[force] for multiple attributes, you need to wrap the line, starting with the first property, one row per property.

``` JavaScript
No child nodes
<somecomponent
Longprop={longprop}
Anotherlongprop={anotherlongprop}
/>

Has child nodes
<somecomponent
Longprop={longprop}
Anotherlongprop={anotherlongprop}
>
<somechild/>
<somechild/>
</SomeComponent>
```

-[force] use double quotes (' "") as a property of the literal value of the string, using single quotes (' ') in strings in other types of expressions.

``` JavaScript
Bad
<foo bar= ' Bar '/>
<foo style={{width: "20px"}/>

,
<foo bar= "Bar"/>
<foo style={{width: ' 20px '}/>
```

-[Force] add a space before the '/> ' of the closed label.

``` JavaScript
Bad
<foo bar= "Bar"/>
<foo bar= "Bar"/>

,
<foo bar= "Bar"/>
```

-[force] for attributes with a value of ' true ', omit the value portion.

``` JavaScript
Bad
<foo Visible={true}/>

,
<foo Visible/>
```

-[Force] provide a value that uniquely identifies as the ' key ' attribute to the occasion where a ' key ' is used, prohibiting the use of properties that may vary, such as indexes.

The ' key ' attribute is an important attribute of the react when the list is updated, such as the property will change, rendering performance and * * * correctness * can not be guaranteed.

``` JavaScript
Bad
{list. Map (item, index) => <foo Key={index}}

,
{list. map (item => <foo key={item. ID})}
```

-[recommended] Avoid using object and function expressions directly in JSX property values.

' Purecomponent ' uses [' shallowequal '] (https://github com/facebook/fbjs/blob/master/packages/fbjs/src/core/shallowequal. js) to compare ' props ' and ' state ' to determine whether to render, and to use objects in JSX attribute values, The function expression causes the object reference to be different every a times, thus ' shallowequal ' returns ' false ', resulting in unnecessary rendering.


``` JavaScript
Bad
Class Warnbutton {
Alertmessage (message) {
alert (message);
}

Render () {
return <button = the "button" onclick={() => this alertmessage prompt </button>
}
}

,
Class Warnbutton {
@autobind
Alertmessage () {
Alert (this. props);
}

Render () {
return <button = "button" onclick={this. alertmessage}> hint </button>
}
}
```

-[recommended] to control the JSX level within 3 floors.

JSX provides a reusable form of component-based portability, so you can nicely split large and complex structures by encapsulating a portion of the structure as a function component. The structure of the level too deep can bring the disadvantage of too much indentation and readability decline. As with the number of lines of code within the control function and the branch level, controlling the level of the JSX can effectively improve the maintainability of the code.

```JavaScript
Bad
Let List = ({items}) => (
<ul>
{
Items. Map (item => (
<li>
<header>
<h3>{item. title}</h3>
<span> {item. subtitle} </span>
</header>
<section> {item. Content} </section>
<footer>
<span> {item. author} </span> @ <time> {item. posttime} </time>
</footer>
</li>
))
}
</ul>
);

,
Let Header = ({title, subtitle}) => (
<header>
<h3>{title}</h3>
<span> {subtitle} </span>
</header>
);

Let Content = ({content}) => <section> {content} </section>;

Let Footer = ({author, posttime}) => (
<footer>
<span> {author} </span> @ <time> {posttime} </time>
</footer>
);

Let item = Item => (
<div>
<header {... item}/>
<content {... item}/>
<footer {... item}/>
</div>
);

Let List = ({items}) => (
<ul>
{Items. Map (Item)}
</ul>
);
```
