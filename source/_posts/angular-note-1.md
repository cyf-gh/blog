---
title: Angular学习笔记 1 组件参数传递
date: 2019-02-16 00:09:57
categories: Angular
---

# 组件之间互传参数

## 父传子（Parent => Child）  

父组件传递

```html
<!-- parent.componet.html -->
<app-child [childVarName]="parentVarName" [parent]="this" [func]="foo"><app-child>
```

传入函数时不需要括号。

接受参数

```typescript
// child.component.ts
import { Component, OnInit, Input } from '@angular/core';
...
export class ChildComponent implements OnInit {
@Input() childVarName:any;
@Input() parent:ParentComponent;
@Input() func:Function;
...
doRun() {
    this.parent.foo();
    this.func();
    // func(); Error
}
}
```

注意Typescript调用本类的成员时都需要用this来限定。

以上代码中的Input Component等被称作为**装饰器（Decorator）**

## 子传父（Child=> Parent）

使用装饰器ViewChild。 

```html
<!-- parent.componet.html -->
<app-child #child><app-child>
```

```typescript
// parent.component.ts
import { Component, ViewChild } from '@angular/core';

export class ParentComponent {
  @ViewChild('child') mChild:any;
  foo() {
    alert( this.mLayout.msg );
  }
}
```



## 广播 Output EventEmitter

```typescript
// child.component.ts
import { Component, OnInit, Output, EventEmitter } from '@angular/core';

export class ChildComponent implements OnInit {
  @Output() private outerInChild = new EventEmitter();
  ngOnInit() {
    // 相当于一个委托，将父组件的方法委托给Output修饰器下的成员
    this.outerInChild.emit("Boardcast from Child");
  }
}
```



```html
<!-- parent.componet.html -->
<app-child (outerInChild)="foo($event)"></app-child>
<!-- ($event) 为广播的数据内容 -->
```

下面我赶紧写了一段cpp代码解释一下广播系统的逻辑。

```c++
// 通俗理解
class Output {
    public:
    emit( const char * msg ) {
		// pesudo code here
        typeof(this) tmp( msg ); // Call parent function
    }
};
class ParentComponent {
    public:
    class foo : public Output {
        public:
        foo( const char * msg) : Output( msg ) {
            // do some stuff
        }  
    };
};

class ChildComponent {
    private:
    	Output *m_pOutput;
    public:
    void foo() {
        m_pOutput.emit("Hello From Boardcast");
    }
};

// ... some place 
// Do same as the html do
{
    ChildComponent* pChild = new ChildComponent;
    pChild.m_pOutput = ParentComponent::foo(); // bind
}
```