# Angular Architecture

> Modules, Components, Templates, Metadata, Services, Dependency Injection

Angular follows a **component-based architecture**, where an application is divided into reusable components. The main building blocks are **Modules, Components, Templates, Metadata, Services, and Dependency Injection (DI)**.

---

## Table of Contents

1. [Modules (NgModule)](#1-modules-ngmodule)
2. [Components](#2-components)
3. [Templates](#3-templates)
4. [Metadata](#4-metadata)
5. [Services](#5-services)
6. [Dependency Injection (DI)](#6-dependency-injection-di)
7. [Overall Angular Architecture](#overall-angular-architecture)
8. [Interview Questions & Answers](#interview-questions--answers)
9. [Quick Revision Table](#quick-revision-table)

---

## 1. Modules (NgModule)

A **Module** is a container that groups related components, directives, pipes, and services. It helps organize the application into logical sections.

### Responsibilities
- Organizes the application
- Declares components
- Imports other modules
- Exports components
- Registers services

### Example

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

### Common Angular Modules

| Module | Purpose |
|---|---|
| `BrowserModule` | Required for browser apps |
| `CommonModule` | `ngIf`, `ngFor` |
| `FormsModule` | Template-driven forms |
| `ReactiveFormsModule` | Reactive forms |
| `HttpClientModule` | HTTP requests |
| `RouterModule` | Routing |

### Standalone Components (Angular 15+)

Modern Angular allows applications without NgModules.

```typescript
@Component({
  standalone: true,
  selector: 'app-home',
  template: `<h1>Hello</h1>`,
  imports: []
})
export class HomeComponent {}
```

> Nowadays many projects prefer **Standalone Components** over modules.

---

## 2. Components

A **Component** is the basic building block of an Angular application. Each component controls one part of the UI.

A component consists of:
- TypeScript class
- HTML template
- CSS styles

### Example

```typescript
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent {
  name = "John";
}
```

```html
<h2>{{name}}</h2>
```

**Output:**
```
John
```

### Component Life Cycle

```
Create Component
      ↓
ngOnChanges()
      ↓
ngOnInit()
      ↓
ngDoCheck()
      ↓
ngAfterContentInit()
      ↓
ngAfterContentChecked()
      ↓
ngAfterViewInit()
      ↓
ngAfterViewChecked()
      ↓
ngOnDestroy()
```

---

## 3. Templates

**Templates** define the UI of a component. Angular templates use HTML plus Angular syntax.

```html
<h1>{{title}}</h1>
```

**Interpolation:**
```html
{{username}}
```

**Property Binding:**
```html
<img [src]="imageUrl">
```

**Event Binding:**
```html
<button (click)="save()">Save</button>
```

**Two-way Binding:**
```html
<input [(ngModel)]="username">
```

**Structural Directives:**
```html
<div *ngIf="isLogin">
  Welcome
</div>

<li *ngFor="let item of items">
  {{item}}
</li>
```

---

## 4. Metadata

**Metadata** tells Angular how to process a class. It is written using **Decorators**.

```typescript
@Component({
  selector: 'app-home',
  templateUrl: './home.html'
})
```

Here `@Component` is metadata.

### Other Decorators

| Decorator | Purpose |
|---|---|
| `@Component` | Defines a component |
| `@NgModule` | Defines a module |
| `@Injectable` | Defines a service |
| `@Directive` | Defines a directive |
| `@Pipe` | Defines a pipe |

---

## 5. Services

**Services** contain business logic that can be shared across multiple components. Instead of writing the same logic in every component, create a service.

### Example

```typescript
@Injectable({
  providedIn: 'root'
})
export class UserService {
  getUsers() {
    return ['John', 'David'];
  }
}
```

```typescript
// Component
constructor(private userService: UserService) {}

users = this.userService.getUsers();
```

### Advantages
- Code reuse
- Separation of concerns
- Easier testing
- Centralized business logic

---

## 6. Dependency Injection (DI)

**Dependency Injection** means Angular creates and provides required objects automatically instead of you creating them manually.

### Without DI

```typescript
export class UserComponent {
  service = new UserService();
}
```

**Problems:**
- Tight coupling
- Difficult to test
- Difficult to replace implementation

### With DI

```typescript
constructor(private service: UserService) {}
```

Angular automatically injects `UserService`.

### How DI Works

```
Need Service
      ↓
Component Constructor
      ↓
Angular Injector
      ↓
Creates Service
      ↓
Returns Instance
```

### Provider Example

```typescript
@Injectable({
  providedIn: 'root'
})
export class UserService {}
```

`providedIn: 'root'` means:
- One instance
- Singleton
- Available throughout the application

### Injecting Service

```typescript
constructor(private userService: UserService) {}
```

Angular automatically provides the instance.

---

## Overall Angular Architecture

```
                Angular Application
                       │
        ┌──────────────┴──────────────┐
        │                             │
     Module (AppModule)        Standalone Component
        │
        ├──────────────┐
        │              │
   Components      Services
        │              │
        │              │
    Templates      Business Logic
        │              │
        └────── Dependency Injection ──────┐
                                            │
                                       Angular Injector
```

---

## Interview Questions & Answers

**Q1. What is Angular Architecture?**

Angular architecture is based on a component-based structure where an application is built using Modules (or Standalone Components), Components, Templates, Metadata, Services, and Dependency Injection. Each part has a specific responsibility, making applications modular, maintainable, and scalable.

**Q2. What is a Module in Angular?**

A Module groups related components, directives, pipes, and services into a single unit. It organizes the application and manages imports, declarations, providers, and bootstrap configuration. In newer Angular versions, Standalone Components can reduce or eliminate the need for NgModules.

**Q3. What is a Component?**

A Component is the fundamental UI building block in Angular. It consists of a TypeScript class for logic, an HTML template for the view, and CSS for styling.

**Q4. What is a Template?**

A Template defines the user interface of a component. It uses HTML enhanced with Angular features like interpolation, property binding, event binding, two-way binding, and structural directives.

**Q5. What is Metadata?**

Metadata uses decorators such as `@Component`, `@Injectable`, and `@NgModule` to tell Angular how to process a class and configure its behavior.

**Q6. What is a Service?**

A Service contains reusable business logic or data access code that can be shared among multiple components, improving code reuse and maintainability.

**Q7. What is Dependency Injection?**

Dependency Injection is a design pattern where Angular automatically creates and injects required dependencies (such as services) into components, reducing coupling and improving testability.

---

## Quick Revision Table

| Building Block | Purpose | Example |
|---|---|---|
| Module | Organizes the application | `AppModule` |
| Component | Controls a part of the UI | `UserComponent` |
| Template | Defines the UI | `user.component.html` |
| Metadata | Configures classes using decorators | `@Component` |
| Service | Contains reusable business logic | `UserService` |
| Dependency Injection | Automatically provides dependencies | Constructor injection |

---

### Easy Way to Remember the Flow

```
Module (or Standalone Component) → Component → Template → Service → Dependency Injection → Browser
```

This flow is a common explanation in Angular interviews and clearly shows how the main building blocks interact.