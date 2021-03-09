<p align="center"><img src="angular.png" width="300px"></p>

<h1 align="center">
    <strong>Angular TodoList</strong>
</h1>
<h3 align="center">
    TodoList app written in Angular
</h3>

<p align="left"><img src="Screenshot.jpg" width="450px"></p>

## Angular
Angular https://angular.io/

Angular is full featured JavaScript framework created & maintained by Google and is used for building front-end applications or the front-end part of a full stack application.

AngularJS was released in 2010. It is not recommended and should be updated to Angular.

Angular refers to version 2+. Right now we are on version 7 but 2-7 is the same framework with a few changes, mostly under the hood.

## Angular gives you
* *Organized front-end structure (Components, Modules, Services)*
* *Extremely powerful & full featured*
* *All-in-one solution (Routing, HTTP, RxJS, etc)*
* *Build powerful SPA apps*
* *MVC - Model, View, Controller design pattern*
* *TypeScript*
* *Fantastic CLI*

## Installing Angular CLI
To check npm version
```
npm --version
```

Install Angular cli
```
npm install -g @angular/cli
```

Add path to your system:\
Control Panel > System > Advanced System Settings > Environment Variables > User Variables > PATH
```
C:\Users\ <USERNAME> \AppData\Roaming\npm
C:\Users\ <USERNAME> \AppData\Roaming\npm\node_modules\@angular\cli\bin
```

To check ng version
```
ng --version
```

## Creating Angular project
On termilan write
```
ng new angular-crash-todolist
```

On routing answer 'Yes'\
After that project folder will be created\

Change to project folder:
```
cd angular-crash-todolist
```

Open current project with VSCode:
```
code .
```

Start 'DEV' server that ng provides.
```
ng serve --open
```

This will open our prjoect's boiler plate on browser

## Project files
packace.json          - it has all depencencies and packages that are included
angular.json          - config file, where you can import bootstrap or local files
src/index.html        - main page
src/styles.css        - styling
app/                  - folder where you create all your components services
app/module.ts         - entrypoint to Angular. All new components has to go there(cli will add automatically). All components will be TypeScript(.ts) files
app/app.component.ts  - has TypeScript decorator. It includes metadata for component. 'app-root' will be displayed on index.html
app/app.component.html- will be displayed inside index.html

## Project
Let's create new component 'Todos'
```
ng generate component components/Todos
```

This will create src/app/components/todos folder with:
* *todos.component.css*\
* *todos.component.html*\
* *todos.component.spec.ts*\
* *todos.component.ts*

On app.component.html we will embed our Todos page by adding component selector(app-todos)
```
<div>
  <app-todos></app-todos>
</div>
```

We'll add 'src/app/models/Todo.ts' file
```
export class Todo {
    id:number;
    title:string;
    completed:boolean;
}
```

And we import it to 'todos.components.ts'
```
import { Todo } from '../../models/Todo';
```

On ngOnInit we will add 3 todos
```
  ngOnInit(): void {
    this.todos = [
      {
        id: 1,
        title: 'Todo One',
        completed: false
      },
      {
        id: 2,
        title: 'Todo Two',
        completed: true
      },
      {
        id: 3,
        title: 'Todo Three',
        completed: false
      }
    ]
  }
```

If you get error 'Property 'id' has no initializer and is not definitely assigned in the constructor.'\
It is because TypeScript 2.7 includes a strict class checking where all the properties should be initialized in the constructor. A workaround is to add the ! as a postfix to the variable name:
```
export class Todo {
    id!:number;
    title!:string;
    completed!:boolean;
}
```

Let's loop thru this array on our 'todos.component.html' with 'ngFor'
```
<ul *ngFor="let todo of todos">
    <li>{{ todo.title }}</li>
</ul>
```

Output will display our todos
* Todo One\
* Todo Two\
* Todo Three\

Let's make every todo a different componenet.}
For that we type on our terminal
```
ng g c components/TodoItem
```

To display different component instead of list item we will use our\
created 'todo-item-component.ts' where selector will be 'app-todo-item'.\
So we change our code
```
<app-todo-item *ngFor="let todo of todos" [todo]="todo">
</app-todo-item>
```

This will give us 'todo' property error\
For that we need to define our property as input in 'todo-item-components'\
by adding input and defining an variable
```
import { Component, OnInit, Input } from '@angular/core';
import { Todo } from 'src/app/models/Todo';

@Component({
  selector: 'app-todo-item',
  templateUrl: './todo-item.component.html',
  styleUrls: ['./todo-item.component.css']
})
export class TodoItemComponent implements OnInit {
  @Input() todo!: Todo;

  constructor() { }

  ngOnInit(): void {
  }
}
```

Now our page will display\
todo-item works!\
todo-item works!\
todo-item works!

To show our items on page in 'todo-item-component.html' instead of
```
todo-item works!
```
We pass our values
```
<p>{{ todo.title }}</p>
```

Page will display\
Todo One\
Todo Two\
Todo Three

