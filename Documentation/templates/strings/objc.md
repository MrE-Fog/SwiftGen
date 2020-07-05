## Template Information

| Name      | Description       |
| --------- | ----------------- |
| File names | strings/objc-string-h.stencil & strings/objc-string-m.stencil |
| Configuration example | <pre>strings:<br />  inputs: path/to/Localizable.strings<br />  outputs:<br />    - templateName: objc-h<br />      output: Localizable.h<br />    - templateName: objc-m<br />      output: Localizable.m</pre> |
| Language | Objective-C |
| Author | Eric Slosser |

## When to use it

- When you need to generate *Objective-C* code.  Perhaps because you have a pure Objective-C project and don't want to add a Swift file to it (thus triggering the inclusion of the Swift runtime into your build).  Or perhaps because you can't find a template that generates Swift that can be accessed from Objective-C.

## Customization

You can customize some elements of this template by overriding the following parameters when invoking `swiftgen`. See the [dedicated documentation](../../ConfigFile.md).

| Parameter Name | Default Value   | Description |
| -------------- | --------------- | ----------- |
| `headerName` | "Localizable.h" | The name of the ObjC header generated by the `objc-string-h` template.  The generated `.m` file will `#include` "{{headerName}}".  This parameter should have the same value as the `output` file name used for the `template: objc-string-h` entry in your config file. |
| `noComments` | N/A | Setting this parameter will disable the comments describing the translation of a key. |

## Generated Code

**Extract:**

```swift
@interface Localizable : NSObject
// alert__message --> "Some alert body there"
+ (NSString*)alertMessage;
// alert__title --> "Title of the alert"
+ (NSString*)alertTitle;
// ObjectOwnership --> "These are %3$@'s %1$d %2$@."
+ (NSString*)objectOwnershipWithValues:(NSInteger)p1 :(NSString*)p2 :(NSString*)p3;
// percent --> "This is a %% character."
+ (NSString*)percent;
...
@end
```

[Full generated code](../../../Tests/Fixtures/Generated/Strings/objc-m/localizable.m)

## Usage example

```objc
// simple strings
NSString* message = Localizable.alertMessage
NSString* title = Localizable.alertTitle

// with parameters, note that each argument needs to be of the correct type
NSString*  apples = [Localizable.applesCountWithValue:3];
NSString*  bananas = [Localizable.bananasOwnerWithValues:5 :@"Olivier"];
```