---
layout: post
title: 'How C# programmer started developing for iPhone'
author: Yura
tags:
    - 'C#'
    - iPhone
    - Objective C
categories:
    - development
    - technology
permalink: /development/how-c-programmer-started-developing-for-iphone.html
---
I have a lot of experience in C# programming. But when I first heard about iPhone, I decides to try to develop something for the device.
<!--more-->
I started with googling about OS iPhone. And found that for start developing for iPhone I will need:

  1. Computer with Mac OS X 10.5.5.
  2. Join the Apple iPhone Developer Program (For starting developing you don't need to pay, but for debugging on device and deploying you have to pay $99).
  3. Get iPhone or iPod Touch.
  4. Download and install the latest version of the iPhone SDK.

First of all I had to get any computer with Mac OS X. The problem was that I'm windows developer and don't have Macs in touch. But I found that I can install Mac OS X on regular computer and it's called "hackintosh". However I didn't do it I bought Mac Book Pro and iPhone. It was expensive but I don't sorry about it. The iPhone is first smart-phone that I satisfied from. I had many smart-phones in past with Symbian and Windows OS but iPhone OS is in some levels high than these operation systems. Mac Book Pro is another story, may be I will write post about it.

The other steps I passed without problems. The problems started when I write first line on Objective C. First of all the way of method calling and passing parameters was took from me any hours of googling. It wasn't seems on other programming languages that I familiar with. In additional there was lot of such problems with syntax of the language. So I want to give a list of parallels between C# and Objective C, for C# programmers starting develop for IPhone.

### Function defenition
C#
```c
int Foo(string param1, int param2) {} 
```
Objective C
```objectivec
(void)Foo:(NSString*)param1 Param2:(NSInteger)Param2 {}
```
### Class defenition
C#
```c    
public class MyClass { 
  public DateTime publicVar;  
  private int privateVar;    
  public int MyProperty { get; set; } 

  public MyClass()  
  { 

  }    

  public MyClass(int param1) 
  { 

  }    

  public void Foo(int param1 , string param2)  
  {  

  }  

  public static void staticFoo(int param1, string param2)  
  { 

  }    

  private void privateFoo(int param1 , string param2)  
  {  

  }  
} 
```
Objective C

MyClass.h
```objectivec      
#import <Foundation/Foundation.h> 

// @interface is like class in C# 
@interface MyClass : NSObject 
{  
  NSDate* _publicVar;  
  @private  NSInteger _privateVar; 
} 
@property (nonatomic) NSInteger MyProperty;   

// Custom initilization
- (id)init:(NSInteger)param1;

- (void)Foo:(NSInteger)param1 Param2:(NSString*)param2;

//The finction is like static in C# 
+ (void)staticFoo:(NSInteger)param1 Param2:(NSString*)param2; 

@end
```
MyClass.m
```objectivec          
#import "MyClass.h"   

@interface MyClass()
- (void)privateFoo:(NSInteger)param1 Param2:(NSString*)param2; 
@end   

@implementation MyClass 
// This line create functions get and set for property 
@synthesize MyProperty;   

// Regular init (override of NSObject init method)
- (id)init 
{  
  if(self = [super init])  
  {  

  }  
  return self; 
}   

- (id)init:(NSInteger)param1 
{  
  if(self = [super init])  
  {  

  }  
  return self; 
}   

-(void)dealloc 
{  
  [super dealloc]; 
}   

- (void)Foo:(NSInteger)param1 Param2:(NSString*)param2 
{ 

}   

+ (void)staticFoo:(NSInteger)param1 Param2:(NSString*)param2 
{ 

}   

- (void)privateFoo:(NSInteger)param1 Param2:(NSString*)param2 
{ 

}  

@end 
```
### Creating object
C#
```c
MyClass myClassA = new MyClass();  
// Custom initilization  
MyClass myClassB = new MyClass(1); 
```
Objective C
```objectivec                 
MyClass* myClassA = [[MyClass alloc] init];  
// Custom initilization  
MyClass* myClassB = [[MyClass alloc] init:1]; 
```
When you creating objects by "alloc", don't forget to release it. But never don't call dealloc derectly. For more information about memory management: [Memory Management Basics Tutorial Video](http://www.markj.net/iphone-memory-management-tutorial-video/).
                    
### Calling for methods
C#
```c                     
myClassA.Foo(1, "something");  
// Calling to static method  
MyClass.staticFoo(1, "something"); 
```
Objective C
```objectivec
[myClassA Foo:1 Param2:@"something"];  
// Calling to static method  
[MyClass staticFoo:1 Param2:@"something"]; 
```
### Catch Exeptions
C#
```c
MyClass myClass = new MyClass();  
try  
{  
  myClass.Foo(1,"something");  
}  
catch(Exception exp)  
{  
  // Output to log  
} 
```
Objective C
```objectivec
MyClass *myClass = [[MyClass alloc] init];  
@try 
{  
  [myClass Foo:1 Param2:@"something"];  
}  
@catch (NSException *exception) 
{  
  NSLog(@"Exception: %@: %@", [exception name], [exception reason]);  
}  
@finally 
{  
  [myClass release];  
}
```
### Throw Exeptions
C#
```c
Exception exp = new Exception("Some message");  
throw exp; 
```
Objective C
```objectivec
NSException *exp = [NSException exceptionWithName:@"SomeTypeOfExeption"  reason:@"Some message" userInfo:nil];  
@throw exp; 
```
### Interface 
There is no interface in objective C. But I sometimes use protocol like interface.
C#
```c
public interface MyInterface  
{  
  void Foo(int param1, object param2);  
}  

public class MyClass : MyInterface  
{  
  public MyClass()  
  {  

  }    
  
  public void Foo(int param1, object param2)  
  {  

  }    
} 
```
Objective C
```objectivec
@protocol MyProtocol   
// It say that methods is optional for implementation  
@optional  
- (void)Foo:(int)param1 Param2:(id)param2;  
@end    

@interface MyClass : NSObject   
{  

}  
- (void)Foo:(int)param1 Param2:(id)param2;  
@end 
```
### Helpfull links:
- [Stanford University iPhone Application Programming (CS 193P)](http://www.stanford.edu/class/cs193p/cgi-bin/index.php) - The cource is all that you need for start programming.
- [iPhone Dev Center](http://developer.apple.com/iphone/)
- [The Objective-C 2.0 Programming Language](http://developer.apple.com/documentation/Cocoa/Conceptual/ObjectiveC/ObjC.pdf)
- [Object-Oriented Programming with Objective-C](http://developer.apple.com/documentation/Cocoa/Conceptual/OOP_ObjC/OOP_ObjC.pdf)

