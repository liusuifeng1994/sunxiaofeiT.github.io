---
layout: blog
istop: true
front: true
title: "谈谈前端框架 Angular 的组件"
background-image: "../img/angularzujian-0.jpg"
date: 2017-10-31 15:30:00
category: angular
tags:
- angular
- 前端框架
- angular组件
---

# 谈谈 anguler 框架中的组件

---

组件负责控制屏幕上的某一块区域，我们也称这块区域为视图，即组件是用来控制视图显示的逻辑。

我们在类中定义组件的应用逻辑，为视图提供支持。组件通过一些由属性和方法组成的API与视图交互。

## 编写组件

---

首先在命令行中输入：
```
npm start
```
或
```
ng serve
```
来启动应用，当我们改变了代码时，它会自动编译，并刷新浏览器页面。

#### 组件的命名

* 组件的类名应该是`大驼峰形式` ，并且以 Component 结尾。例如一个显示英雄详细信息的组件名称为`HeroDetailComponent`。
* 组件的文件名应该是`小写中线形式`，每个单词使用中线分隔，并且以`.component.ts` 结尾。

#### 组件引入的包

组件的文件中需要引入名叫 Component 包。

例如，HeroDetailComponent组件中肯定需要包含这样一行代码：

> import { Component } from '@angular/core';

请注意：要定义一个组件，总是要先导入符号 Component。

#### 第一个组件

我们不用手动新建文件，第一章安装过的 `Angular/cli` 工具可以帮助我们完成新建一个组件文件的工作。
在新建文件之前，我们先来看一下当前的文件目录。
```
|---e2e
|   |---app.e2e-spec.ts
|   |---app.po.ts
|   |---tsconfig.e2e.json
|---node_modules                 存放各种引用的模块包的文件夹
|---src
|   |---app                      应用的根目录，我们要编写的东西基本都在这个文件夹中
|   |---assets                   存放静态资源（图片，视频等）的文件夹
|   |---environments             环境配置文件的存放目录
|   |---favicon.ico              图标
|   |---index.html               应用的入口页面
|   |---main.ts                  应用的入口 ts 文件
|   |---polyfills.ts             
|   |---styles.css               全局的样式文件
|   |---tsconfig.app.json        TypeScript配置文件
|   |---tsconfig.spec.json
|   |---typings.d.ts
|---.angular-cli.json            Angular/cli 的配置文件
|---.editorconfig
|---.gitgnore                    git 的配置文件
|---karma.conf.js
|---package.json                 node 打包的配置文件
|---protrator.conf.js
|---README.md                    项目的说明文件
|---tsconfig.json
|---tslint.json
```

实际上在开发中，我们关注的只有`src`目录。

下面我们开始新建第一个组件，这个组件的作用是在页面中显示一个`Hero`的信息。

命令行中进入该项目目录，使用命令 `ng g component hero` 新建组件文件。

> 这里的 `ng g component hero` 是工具 `angular/cli`的命令，使用了简写，不适用简写时的语句是这样 `ng generate component hero`，参数`generate`是说明要生成文件，参数 `component`是说明要生成一个组件，`hero`当然就是我们要生成组件的名字。更多用法可以查看[说明](https://www.npmjs.com/package/@angular/cli)。

我们可以看到输出：

```
installing component
  create src\app\vip\vip.component.css
  create src\app\vip\vip.component.html
  create src\app\vip\vip.component.spec.ts
  create src\app\vip\vip.component.ts
  update src\app\app.module.ts
```

说明`angular/cli`工具已经帮我们在`app`下新建一个`vip`文件夹，4个文件。

```js
|---hero.component.css           是CSS样式文件
|---hero.component.html          是html文件
|---hero.component.spec.ts       是测试文件，我们开发过程中几乎用不到
|---hero.component.ts            是我们需要的vip组件文件
```

打开`vip.component.ts`文件：
```js
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-hero',
  templateUrl: './vip.component.html',
  styleUrls: ['./vip.component.css']
})
export class VipComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

}
```

> 这些都是`angular/cll`工具自动填写的。
> - `selector`属性是CSS选择器的名字， `app-hero` 会匹配元素的标签名，用于在父组>件中的模板中标记出当前组件的位置。（在父组件中使用标签`<app-hero></app-hero>` 即可调用`VipComponent`组件。
> - `temlpateUrl`属性是外联`HTML`文件
> - `stylesUrls`属性是外联样式`CSS`文件。

##### 显示会员名字

1. 先把第一章的`Hello World`删除。
    - 将`app.component.ts`中的`title`属性删除
    - 将`app.component.html`全部删除
    - 将`index.html`中的`<title>Hello</title>`改为`<title>my first angular app</title>` 
    这时候，打开浏览器，可以发现页面变成了空白，标题变成了 `my first angular app` 。

2. 打开`hero.component.ts`，添加变量`vipName`。
    ```js
    export class VipComponent implements OnInit {

    constructor() { }

    vipName = 'hero';

    ngOnInit() {
    }

    }
    ```

3. 打开`hero.component.html`。

    - 删除原有内容
    - 添加`<h1>Hello {{vipName}}!</h1>`
    > 这里的双大括号是Angular中的插值表达式绑定语法。它们表示的组件中的`hero`属性的值会作为字符串插入到HTML中间。
    > 这个文件中的代码称为模板，我们通过组件的自带的模板定义组件视图。模板以html形式存在，告诉Angular如何渲染组件。多数情况下，模板看起来很像标准的HTML，但是也有不同的地方。

4. 打开`app.component.html`。

    - 添加`<app-hero></app-hero>`

5. 打开浏览器，可以看到：

    ![img](/assets/chapter2/hellovip.png)

目前为止，一个显示`Hello hero`的组件已经做好了。

下面我们来改进这个组件。

##### 英雄对象

显然，一个会员有许多属性，所以我们需要把`hero`从一个字符串变量换成一个类。
创建一个`Hero`类，它具有`id`、`name`、`gender`、`desc`属性。分别表示一个英雄的id，姓名，性别，相关描述。
现在，把下列代码放到`hero.component.ts`的顶部，仅次于import语句。

```js
export class Hero {
    id: number;
    name: string;
    gender: string;
    desc: string;
}
```

> 一般我们总是 `export`组件类，应为我们肯定会在别的地方`import`它。

现在，有了一个`Hero`类，我们把组件的`heroName`属性换成类型为`Hero`的`hero`属性。然后以`1`为 id ，以`王小明`为 name ，初始化它。

```js
hero: Hero = {
    id: 1,
    name: '王小明',
    gender: 'man',
    desc: 'I am a student. I like study.'
}
```

我们把`HeroName`属性换成了`hero`属性，所以也要更新模板中的绑定表达式，来引用`hero`的两个属性。

> 文件：hero.component.html
```html
<h1>Hello {{hero.name}}!</h1>
<h2>Your id is: {{hero.id}}</h2>
```

打开浏览器，我们可以看到修改后的结果了。

![图片可能是被吃了](/assets/chapter2/helloyourid.png)


##### 编辑会员的名字

用户应该能在一个`<input>`输入框中编辑会员的名字。当用户输入时，这个输入框应该能同时显示和修改英雄的`<name>`属性
也就是说，我们要在表单元素`<input>`和组件`<hero.name>`属性之间建立双向绑定。

##### 双向绑定

打开`hero.component.html`文件，修改内容为：
```html
<h1>Hello {{hero.name}}!</h1>
<h2>Your id is {{hero.id}}</h2>
<div>
    <label>name：</label>
    <input [(ngModel)]="hero.name" placeholder="name">
</div>
<div>
    <label>id：</label>
    <input [(ngModel)]="hero.id" placeholder="name">
</div>
```
> `[(ngModel)]` 是一个Angular语法，用与把`hero.name`绑定到输入框中，它的数据流是双向的：从属性到输入框，从输入框回到属性。
> 要使用`[(ngModel)]`，我们必须导入`FormsModule`模块。

##### 导入 FormsModule

打开`app.module.ts`文件，从`@angular/forms`导入符号`FormsModule`。然后把`FormsModule`添加到`@NgModule`元数据的`imports`数组中，它是当前应用正在使用的外部模块列表。

修改后的`app.module.ts`:

```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { HeroComponent } from './hero/hero.component';

@NgModule({
  declarations: [
    AppComponent,
    VipComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

> 关于`FormsModule`和`ngModel`的更多知识，可以查看[表单](https://angular.cn/guide/forms#ngModel)和[模板语法](https://angular.cn/guide/template-syntax#ngModel)

打开浏览器，可以看到：
![图片可能是被吃了](/assets/chapter2/3.png)

我们可以修改`hero`的名字和id，可以看到这个改动立刻体现在上方的内容中。


*现在我们已经新建了一个组件，来显示一个会员的信息。*
*实际情况是我们需要管理多个会员，所以下面我们来扩展这个实例，让它显示会员列表，允许用户来选择一个会员，查看该会员的详细信息。*

#### 扩展组件

##### 调整组件结构

Angular官方指导建议一个`ts`文件中只有一个类，所以我们将之前的组件中的类放到新的文件中。

######　将`Hero`类放到新文件中

- 使用命令`ng g class domain/hero`新建`Hero`类的文件。
- 将`hero.component.ts`中的`Hero`类的内容剪切到新建的文件中。
- 在`hero.component.ts`中添加`import { Hero } from '../domain/hero'`。

> 在这里domain文件夹用来存放对象类文件

现在，`hero.component.ts`文件是：
```js
import { Component, OnInit } from '@angular/core';

import { Hero } from '../domain/hero';

@Component({
  selector: 'app-hero',
  templateUrl: './hero.component.html',
  styleUrls: ['./hero.component.css']
})
export class HeroComponent implements OnInit {

  constructor() { }

  hero: Hero = {
    id: 1,
    name: '王小明',
    gender: 'man',
    desc: 'I am a student. I like study.'
  };

  ngOnInit() {
  }
}
```

`hero.ts`文件是：
```ts
export class Hero {
    id: number;
    name: string;
    gender: string;
    desc: string;
}
```

##### 模拟数据

要想显示更多的`hero`信息，我们就需要获取一些hero数据，当然在实际情况中是从web服务器中获取数据，但现在我们用一个数组模拟web api。在后续的章节中，我们后介绍到web api的使用。

在app目录下新建一个文件`mock-heroes.ts`，在这个文件中我们添加一个`hero`数组：
```js   
import { Hero } from './domain/hero';
 
export const HEROES: Hero[] = [
    { id: 1, name: 'Mr.Nice' , gender: 'man', desc: 'I am Mr.Nive. I like apple.'},
    { id: 2, name: 'Narco' , gender: 'man', desc: 'I am Narco. I like banana.'},
    { id: 3, name: 'Bombasto' , gender: 'man', desc: 'I am Bombasto. I like orange.'},
    { id: 4, name: 'Celeritas', gender: 'man', desc: 'I am Celeritas. I like grape.'},
    { id: 5, name: 'Magneta', gender: 'man', desc: 'I am Magneta. I like strawberry.'},
    { id: 6, name: 'RubberMan', gender: 'man', desc: 'I am RubberMan. I like pears.'},
    { id: 7, name: 'Dynama', gender: 'man', desc: 'I am Dynama. I like tomato.'},
    { id: 8, name: 'Dr IQ', gender: 'man', desc: 'I am Dr IQ. I like peach.' },
    { id: 9, name: 'Magma', gender: 'man', desc: 'I am Magma. I like sandwich.'},
    { id: 10, name: 'Tornado', gender: 'man', desc: 'I am Tornado. I like hamburger.'}
];
```
> 别忘了`import Hero`,因为`hero`类在另一个`hero.ts`中。

##### 改变会员属性

在`hero.component.ts`文件中，添加一个公共属性，用来暴露这些`hero`，以供绑定。
```js
import { Component, OnInit } from '@angular/core';

import { Hero } from '../domain/hero';
import { HEROES } from '../mock-heroes';

@Component({
  selector: 'app-hero',
  templateUrl: './hero.component.html',
  styleUrls: ['./hero.component.css']
})

export class VipComponent implements OnInit {

  constructor() { }

  heroes = HEROES;
  selectedHero: Hero;

  ngOnInit() {
  }

}
```

> 在这里，我们没有明确定义`heroes`属性的数据类型，是因为Typescript能从`HEROES`推断出来。


##### 改变视图模板

我们在模板中用一个无序列表来显示会员的名字。
打开`hero.component.html`文件，添加一下代码：
```html
<h2>All heroes</h2>
<ul class="heroes">
  <li>
    <!-- each hero will be showed here -->
  </li>
</ul>
```
然后需要做的就是将我们模拟的数据填充到这个模板中去。

####### 使用`ngFor`来显示会员列表

我们想要把`HEROES`数组绑定到模板中，迭代并逐个显示它们。

- 修改`<li>`标签，添上内置指令`*ngFor`。
```js
<li *ngFor="let hero of heroes">
```

> ngFor的*前缀表示<li>及其子元素组成了一个主控模板。
> ngFor指令在HeroComponent.heroes属性返回的heroes数组上迭代，并输出此模板的实例。
> 引号中赋值给ngFor的那段文本表示“从heroes数组中取出每个英雄，存入一个局部的hero变量，并让它在相应的模板实例中可用”。
> 要了解更多关于ngFor和模板输入变量的知识，查看[用*ngFor显示数组属性](https://angular.cn/guide/displaying-data#ngFor)和[模板语法章ngFor](https://angular.cn/guide/template-syntax#ngFor)。

这时候，我们打开浏览器可以看到，有了英雄的列表。

![图片可能是被吃了](/assets/chapter2/heroesList.png)

#### 增加英雄详情

我们希望在刚才的英雄列表中点击一个英雄，可以展示这个我们点击的英雄的详情。为实现这个功能，我们需要为英雄列表添加一些样式、添加一个属性用来标示哪个`hero`是被选中的、增加一个展示英雄详情的组件、把`heroDetailComponent`组件添加到`heroComponent`组件中去。

##### 为英雄列表添加样式

打开`hero.component.css`文件，添加样式：
```css
.selected {
  background-color: #CFD8DC !important;
  color: white;
}
.heroes {
  margin: 0 0 2em 0;
  list-style-type: none;
  padding: 0;
  width: 15em;
}
.heroes li {
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  height: 1.6em;
  border-radius: 4px;
}
.heroes li.selected:hover {
  background-color: #BBD8DC !important;
  color: white;
}
.heroes li:hover {
  color: #607D8B;
  background-color: #DDD;
  left: .1em;
}
.heroes .text {
  position: relative;
  top: -3px;
}
.heroes .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: -4px;
  height: 1.8em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```
打开浏览器，我们可以看到英雄列表的样式发生了变化。

![图片可能是被吃了](./assets/chapter2/heroesListcss.png)

##### 添加属性

打开`hero.component.ts`文件，在`heroes = HEROES`下行添加
```js
selectedHero : hero;
```
我们添加了一个用来标识哪个英雄是选中的属性。

##### 增加英雄详情组件

- 在命令行中进入工程目录，使用`Angular/cli`工具新建一个`Component`。
```
ng g component hero-detail
```

- 打开`hero-detail.component.ts`，添加一个属性`hero: Hero`，这就是我们要显示详情的英雄。我们知道这个`hero`属性应该由父组件来传递过来，所以`hero`属性是一个输入属性，将它改写为`@Input hero: Hero`。

> 了解属性的更多知识，查看[属性型指令](https://angular.cn/guide/attribute-directives#why-input).

现在，`hero`属性是`heroDetailComponent`中的唯一的东西，它所做的就是通过它的输入属性`hero`接受一个对象，然后把这个属性绑定到自己的模板中。

下面是完整的`hero-detai.component.ts`文件：
```js
import { Component, OnInit } from '@angular/core';
import { Input } from '@angular/core';

import { Hero } from '../classes/hero';

@Component({
  selector: 'app-hero-detail',
  templateUrl: './hero-detail.component.html',
  styleUrls: ['./hero-detail.component.css']
})
export class HeroDetailComponent implements OnInit {

  @Input() hero: Hero;
  constructor() { }

  ngOnInit() {
  }

}
```

- 打开`hero-detail.component.html`文件，添加：

```html
<div *ngIf="hero">
    <h2>{{hero.name}}'s details!</h2>
    <div><label>id: </label>{{hero.id}}</div>
    <div>
      <label>name: </label>
      <input [(ngModel)]="hero.name" placeholder="name"/>
    </div>
    <div>
      <label>gender: </label>
      <input [(ngModel)]="hero.gender" placeholder="gender">
    </div>
    <div>
      <label>description：</label>
      <input [(ngModel)]="hero.desc" placeholder="description" class="layui-input">
</div>
```

我们使用` ngIf `隐藏空的详情,当应用加载时，我们会看到一个英雄列表，但还没有任何英雄被选中。这时。如果不使用`ngIf`，浏览器会报这样的错误：
```
EXCEPTION: TypeError: Cannot read property 'name' of undefined in [null]
```
所以，我们要在选中英雄之前，把这些英雄的详情留在DOM之外，所以把模板中的英雄详情内容区放在一个<div>中。 然后，添加一个ngIf内置指令，把ngIf的值设置为组件的selectedHero属性。

##### 把`HeroDetailComponent`添加到`HeroComponent`中

- 把<hero-detail>元素添加到AppComponent模板的底部，那里就是英雄详情视图所在的位置。

```html
<h1>{{title}}</h1>
  <h2>My Heroes</h2>
  <ul class="heroes">
    <li *ngFor="let hero of heroes"
      [class.selected]="hero === selectedHero"
        (click)="onSelect(hero)">
      <span class="badge">{{hero.id}}</span> {{hero.name}}
    </li>
  </ul>
<hero-detail [hero]="selectedHero"></hero-detail>
```
> - `<hero-detail [hero]="selectedHero"></hero-detail>`是将selectedHero属性传给组件`HeroDetailComponent`。在等号的左边，是方括号围绕的hero属性，这表示它是属性绑定表达式的目标。我们要绑定到的目标属性必须是一个输入属性，否则Angular会拒绝绑定，并抛出一个错误。而HeroDetailComponent中的`hero`属性在上边我们声明时就是输入属性。
> - 圆括号标识`<li>`元素上的click事件是绑定的目标。 等号右边的onSelect(hero)表达式调用HeroComponent的onSelect()方法，并把模板输入变量hero作为参数传进去。 它是我们前面在ngFor指令中定义的那个hero变量。



##### 添加点击事件
- 在`HeroComponent`文件中添加`onSelect`方法。

打开`hero.component.ts`文件，添加：
```js
onSelect(hero: Hero): void {
    this.selectedHero = hero;
  }
```

- 修改`hero.component.html`文件

将
```js
<li *ngFor="let hero of heroes"
    [class.selected]="hero === selectedHero"
    <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>
```
修改为

```js
<li *ngFor="let hero of heroes"
    [class.selected]="hero === selectedHero"
        (click)="onSelect(hero)">
    <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>
```

> 新建一个英雄详情的组件而不是在HeroComponent中写的好处：代码复用，新建的英雄详情的组件可以重复调用。

点击列表中的一个英雄，可以看到：

![图片可能是被吃了](./assets/chapter2/4.png)