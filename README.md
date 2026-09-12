![Thumbnail](https://media.licdn.com/dms/image/v2/D4D22AQEXh4NlRZbmNQ/feedshare-shrink_800/B4DaBrFnUzIEAc-/0/1788503029283?e=1790812800&v=beta&t=4ju74X8dyxa7y4abb3_qoH1sAwauY1MoGtnGdhQ5vhw)

# ⚡ Angular Interview Questions & Answers

**🚀 MNC Interview Preparation Guide · 2026 Edition**
*Curated by Code with Krishna*

**128** Unique Questions · **15** Topic Areas · **100%** Real MNC Asked

`Angular 17+` `Signals` `RxJS / Operators` `NgRx` `Change Detection` `HTTP Interceptors` `TypeScript` `Performance` `JWT / Auth` `Micro Frontend` `JavaScript Core` `Coding Challenges` `Standalone Architecture` `SSR / Universal`

> Compiled from 20+ real MNC interview posts.

---

## 📋 Table of Contents

⏱️ **Estimated Study Time:** 20–25 hrs to master all 128 questions
Skim in 2–3 hrs · Moderate prep 8–10 hrs · Deep mastery (with coding) 20–25 hrs
*Angular Core + Signals = highest priority for MNCs*

128 unique questions compiled from 20 real LinkedIn MNC interview posts · Deduplicated · Organized by topic · With answers

| # | Section | Range |
|---|---------|-------|
| 🏗️ 1 | [Angular Core Concepts](#-section-1-angular-core-concepts) | Q1–Q12 |
| 🔄 2 | [Change Detection](#-section-2-change-detection) | Q13–Q22 |
| 📡 3 | [Angular Signals](#-section-3-angular-signals) | Q23–Q30 |
| 📦 4 | [Component Communication](#-section-4-component-communication) | Q31–Q37 |
| 📝 5 | [Forms](#-section-5-forms) | Q38–Q44 |
| 🗺️ 6 | [Routing & Guards](#️-section-6-routing--guards) | Q45–Q52 |
| 💉 7 | [Dependency Injection](#-section-7-dependency-injection--services) | Q53–Q58 |
| 🌐 8 | [HTTP & Interceptors](#-section-8-http--interceptors) | Q59–Q66 |
| 🔃 9 | [RxJS & Observables](#-section-9-rxjs--observables) | Q67–Q74 |
| 🏪 10 | [State Management / NgRx](#-section-10-state-management--ngrx) | Q75–Q80 |
| ⚡ 11 | [Performance Optimization](#-section-11-performance-optimization) | Q81–Q86 |
| 🏛️ 12 | [Architecture & Advanced](#️-section-12-angular-architecture--advanced) | Q87–Q96 |
| 🔐 13 | [Authentication & Security](#-section-13-authentication--security) | Q97–Q100 |
| 💛 14 | [JavaScript Fundamentals](#-section-14-javascript-fundamentals) | Q101–Q114 |
| 💻 15 | [TypeScript & Coding](#-section-15-typescript--coding-challenges) | Q115–Q128 |

---

## 🏗️ Section 1: Angular Core Concepts
*Q1 – Q12*

### 1. What are the building blocks of Angular?

- **Components** — Basic UI blocks with template, styles, and logic.
- **Modules (NgModule)** — Group components/directives/pipes/services (optional in Angular 17+ with standalone).
- **Services** — Shared business logic injected via DI.
- **Directives** — Extend HTML (structural: `*ngIf`, `*ngFor`; attribute: custom).
- **Pipes** — Transform template data.
- **Routing** — Navigation between views.
- **Dependency Injection** — Framework for providing and consuming services.

### 2. What is a Module? With standalone component architecture, do we still need modules?

**NgModule** groups declarations, imports, exports, and providers. Since Angular 14+ (default in 17+), **standalone components** can import dependencies directly with `standalone: true`, eliminating the need for NgModules. Modules still work but are no longer required.

> ✅ Modern Angular projects default to standalone. `AppModule` is replaced by `bootstrapApplication()` in `main.ts`.

### 3. What are lifecycle hooks in Angular? List the most important ones.

- `ngOnChanges` — Runs when `@Input` changes (before `ngOnInit`).
- `ngOnInit` — Runs once after component init; best place for API calls.
- `ngDoCheck` — Every change detection cycle.
- `ngAfterContentInit` — After `ng-content` projected.
- `ngAfterViewInit` — After view + child views init; use for `ViewChild` access.
- `ngOnDestroy` — Before destroy; clean up subscriptions here.

> ✅ Most asked: `ngOnInit`, `ngOnDestroy`, `ngOnChanges`, `ngAfterViewInit`

### 4. What is data binding in Angular? Explain all types.

- **Interpolation:** `{{ value }}` — Component → Template.
- **Property binding:** `[src]="url"` — Component → Template.
- **Event binding:** `(click)="handler()"` — Template → Component.
- **Two-way binding:** `[(ngModel)]="value"` — Both directions (requires `FormsModule`). Known as "banana in a box" syntax.

### 5. What is lazy loading in Angular? How is it implemented?

Lazy loading loads modules/components only when the user navigates to them — reducing initial bundle size and improving startup performance.

```ts
// routes.ts — loadChildren (module-based)
{ path: 'admin', loadChildren: () =>
    import('./admin/admin.module').then(m => m.AdminModule) }

// Angular 17+ — loadComponent (standalone)
{ path: 'dashboard', loadComponent: () =>
    import('./dashboard.component').then(c => c.DashboardComponent) }
```

### 6. What is the difference between AOT and JIT compilation?

| Feature | AOT (Ahead of Time) | JIT (Just in Time) |
|---|---|---|
| When compiled | At build time | At runtime in browser |
| Performance | Faster rendering | Slower first load |
| Bundle size | Smaller (no compiler shipped) | Larger |
| Error detection | At build time | At runtime |
| Default | Production (Angular 9+) | Development only |

### 7. What is View Encapsulation in Angular? Explain all three types.

- **Emulated (default)** — Angular adds unique attributes to scope CSS to the component. Styles don't leak in/out.
- **None** — No encapsulation. CSS becomes global. Use cautiously.
- **ShadowDom** — Uses browser's native Shadow DOM for true, strict style isolation.

> 💡 Use Emulated for components, None only for global overrides, ShadowDom for fully isolated web components.

### 8. What is ng-content and how does content projection work?

`ng-content` projects HTML from a parent into a child component's template — enabling flexible, reusable component slots.

```html
<!-- card.component.html -->
<div class="card">
  <ng-content select="[header]"></ng-content>  <!-- named slot -->
  <ng-content></ng-content>                    <!-- default slot -->
</div>

<!-- parent -->
<app-card><h2 header>Title</h2><p>Body content</p></app-card>
```

### 9. What is ngTemplate and ng-container? How do you pass data to ngTemplate?

- `ng-template` — Template block not rendered by default. Rendered via `ngTemplateOutlet` or structural directives.
- `ng-container` — Logical grouping without adding DOM nodes, useful for applying multiple structural directives.

```html
<ng-template #tmpl let-user="user">
  <p>Hello {{ user.name }}</p>
</ng-template>
<ng-container *ngTemplateOutlet="tmpl; context: { user: currentUser }">
</ng-container>
```

### 10. What is tree shaking in Angular?

Tree shaking removes unused code (modules, functions) from the final bundle at build time. Angular's build toolchain (webpack / esbuild in Angular 17+) statically analyzes imports and eliminates dead code.

> ✅ Best practice: Import only specific RxJS operators, use standalone components (more tree-shakable than NgModules), avoid barrel imports of entire libraries.

### 11. What are Pure vs Impure Pipes? What is PipeTransform?

`PipeTransform` interface requires implementing `transform(value, ...args)`.

| | Pure Pipe (default) | Impure Pipe (`pure: false`) |
|---|---|---|
| Re-runs when | Input reference changes | Every change detection cycle |
| Performance | Excellent (cached) | Expensive (runs constantly) |
| Use for | Immutable data / primitives | Arrays/objects with internal mutations |

### 12. What are the new features in Angular 17 to latest versions?

- **Standalone components** (default) — No NgModule needed.
- **Signals** — Fine-grained reactive primitives replacing zone.js dependency.
- **New control flow** — `@if`, `@for`, `@switch` replacing `*ngIf`, `*ngFor`, `ngSwitch`.
- **Deferrable views** — `@defer` for lazy-loading template chunks.
- **Zoneless experiments** — Running Angular without zone.js using Signals.
- **esbuild** — Much faster builds.
- **SSR improvements** — Better hydration, partial hydration.
- **@let** template variables (v18+).
- **Signal inputs/outputs** (v17.1+).

---

## 🔄 Section 2: Change Detection
*Q13 – Q22*

### 13. What is Change Detection in Angular and why does it exist?

Change Detection is Angular's mechanism to synchronize the component data model with the view (DOM). It runs after every asynchronous event (user interaction, HTTP response, timer) and checks if data has changed to update the DOM accordingly.

> 💡 Angular uses a component tree — change detection traverses from root to leaf checking each component.

### 14. What is Zone.js and what role does it play in Change Detection?

Zone.js is a library that monkey-patches asynchronous browser APIs (`setTimeout`, `addEventListener`, XHR, Promises) to notify Angular when an async operation completes. Angular wraps the app in `NgZone`, which triggers change detection automatically after each async task.

> ✅ With Signals (Angular 17+), zone.js dependency is being phased out. Zoneless apps use signals to track reactivity precisely.

### 15. What are the two Change Detection strategies in Angular?

- **Default** — Every component in the tree is checked on every CD cycle. Simple but can be slow for large apps.
- **OnPush** — Component is checked only when: (1) an `@Input` reference changes, (2) an event originates from that component, (3) an Observable via async pipe emits, or (4) `detectChanges()` / `markForCheck()` is called manually.

### 16. What is OnPush strategy? When should you use it?

```ts
@Component({
  selector: 'app-item',
  changeDetection: ChangeDetectionStrategy.OnPush,  // ← add this
  template: `{{ item.name }}`
})
export class ItemComponent {
  @Input() item!: Item;  // Must pass new reference, not mutate
}
```

> ✅ Use with: smart + dumb component pattern, immutable data / spread operators, Observables + async pipe. Great for performance in large lists.

### 17. What is ChangeDetectorRef and what methods does it have?

`ChangeDetectorRef` gives direct control over change detection for a component.

- `detectChanges()` — Immediately runs CD for this component and its children.
- `markForCheck()` — Marks the component (and ancestors) to be checked in the next CD cycle.
- `detach()` — Removes component from CD tree (must call `detectChanges` manually).
- `reattach()` — Re-attaches to CD tree.
- `checkNoChanges()` — Throws error if any changes are detected (dev mode).

### 18. What is the difference between detectChanges() and markForCheck()?

| | `detectChanges()` | `markForCheck()` |
|---|---|---|
| Runs CD | Immediately, synchronously | On next global CD cycle |
| Scope | Component + children only | Component + all ancestors up to root |
| Use when | Async data arrives outside Angular zone | OnPush + data changed via service/Subject |

### 19. What triggers Change Detection in Angular by default?

Zone.js intercepts and triggers CD after: **DOM events** (click, input, scroll), **HTTP requests** (XHR/fetch), **Timers** (`setTimeout`, `setInterval`), **Promises** resolved/rejected, **Router navigation**, and any other async operation Angular knows about via `NgZone`.

### 20. What is detach() in ChangeDetectorRef and why is it powerful?

Calling `cdr.detach()` completely removes a component from Angular's CD tree. The component won't be automatically checked — you control exactly when to run detection by calling `cdr.detectChanges()` manually.

> 💡 Power pattern: Polling dashboards — detach from CD, only call `detectChanges()` when new data arrives. Can dramatically improve performance for complex UIs.

### 21. What is the difference between ApplicationRef.tick() and detectChanges()?

- `ApplicationRef.tick()` — Triggers a full application-wide change detection cycle starting from root. Equivalent to what zone.js calls after each async task.
- `detectChanges()` — Runs CD only for a specific component subtree.

`tick()` is broader and more expensive; use it when you need to trigger global CD from outside Angular's zone.

### 22. Common performance mistakes with Default Change Detection?

1. Using Default strategy everywhere — runs CD on every component for every event.
2. Heavy computations in template expressions or getters (called repeatedly).
3. Not using `trackBy` in `*ngFor` / `@for` — recreates DOM on every change.
4. Using impure pipes where pure pipes suffice.
5. Updating data by mutation instead of immutable patterns (preventing OnPush optimizations).

---

## 📡 Section 3: Angular Signals
*Q23 – Q30*

### 23. What are Signals in Angular? What types do we have?

Signals are reactive primitives that hold a value and notify consumers when the value changes — enabling fine-grained, zone-free reactivity.

- **signal()** — writable signal.
- **computed()** — derived read-only signal.
- **effect()** — side-effect runner when signals change.

```ts
const count = signal(0);          // WritableSignal
const doubled = computed(() => count() * 2); // computed
effect(() => console.log(count())); // runs when count changes
count.set(5);   count.update(v => v + 1);
```

### 24. Are Signals a replacement for RxJS? If not, what is the use of Signals?

**No, Signals are not a full replacement for RxJS.** They serve different purposes:

- **Signals** — synchronous, fine-grained reactivity for state management in components (replace `BehaviorSubject` for simple state, replace zone.js for CD).
- **RxJS** — asynchronous streams, complex operators (`switchMap`, `debounce`, `combineLatest`), event handling, HTTP.

They complement each other. Angular even provides `toSignal()` and `toObservable()` for interop.

> 💡 Use Signals for component state. Use RxJS for async data flows and complex event streams.

### 25. What are Effects in Signals? When to use them?

`effect()` runs a side-effect whenever the signals it reads change. It automatically tracks dependencies.

```ts
effect(() => {
  // Runs whenever 'user' signal changes
  localStorage.setItem('user', JSON.stringify(user()));
});
```

> ⚠️ Don't update signals inside effects — can cause infinite loops. Use `allowSignalWrites: true` only if necessary.

### 26. What are Computed Signals? Give a real-time use case.

`computed()` creates a derived read-only signal that automatically recalculates when its signal dependencies change. It's memoized — only recomputes when inputs change.

```ts
const cart = signal([{price:100},{price:200}]);
const total = computed(() =>
  cart().reduce((sum, item) => sum + item.price, 0)
); // Real use case: cart total auto-updates
```

### 27. How does Change Detection work with Signals (no zone.js dependency)?

With Signals, Angular knows exactly which component reads which signal. When a signal changes, Angular marks only those specific components dirty and re-renders them — without needing zone.js to trigger a global CD cycle. This is called **fine-grained reactivity**. In a fully zoneless app, you opt out of zone.js and Angular relies entirely on Signals for change tracking.

> ✅ Zoneless = faster, less overhead, better performance — the future direction of Angular.

### 28. Explain @Input with Signals, Linked Signal, and use of untrack().

```ts
// Signal input (Angular 17.1+)
name = input<string>();  // read-only signal @Input
name = input.required<string>();

// Linked Signal — writable signal linked to another
source = signal(10);
linked = linkedSignal(() => source() * 2);

// untrack() — read a signal without creating a dependency
effect(() => {
  const a = signalA();  // tracked
  const b = untrack(() => signalB()); // not tracked
});
```

### 29. Difference between signal.set() and signal.update()?

- `set(value)` — Replaces the signal's value with a completely new value.
- `update(fn)` — Updates the value based on the current value (like a functional updater).

```ts
count.set(10);          // set absolute value
count.update(v => v + 1); // increment based on current value
arr.update(list => [...list, newItem]); // immutable add
```

### 30. How do you store API response data in Angular — Signals vs normal variables?

| | Normal Variable | Signal |
|---|---|---|
| Reactivity | Needs zone.js to trigger CD | Automatically triggers targeted CD |
| Template update | Via zone.js / detectChanges | Automatic, fine-grained |
| OnPush compat | Needs `markForCheck()` | Works automatically |
| Recommendation | Legacy code | New Angular 17+ apps |

```ts
users = signal<User[]>([]);
ngOnInit() { this.api.getUsers().subscribe(data => this.users.set(data)); }
```

---

## 📦 Section 4: Component Communication
*Q31 – Q37*

### 31. Various ways of component communication (with and without parent-child relationship)?

- **Parent → Child:** `@Input()` property binding.
- **Child → Parent:** `@Output()` + `EventEmitter`.
- **Parent accessing child:** `@ViewChild`.
- **Sibling / unrelated components:** Shared Service with `BehaviorSubject` / `Subject`, NgRx Store, or Signals.
- **Template variables:** `#ref` for direct template access.

### 32. Use of ViewChild, ContentChild, ViewChildren?

- `@ViewChild` — Query a single element/component/directive from the component's own template. Available from `ngAfterViewInit`.
- `@ContentChild` — Query a single projected content element (`ng-content`). Available from `ngAfterContentInit`.
- `@ViewChildren` — Returns a `QueryList` of all matching elements in the view. Updates dynamically.

### 33. Can we access @Input inside constructor or only in ngOnInit?

With traditional `@Input()`, values are **NOT available in the constructor** — only from `ngOnChanges` and `ngOnInit` onwards. With Signal inputs (`input()` in Angular 17.1+), the signal itself is available in the constructor but its value is set before `ngOnInit`.

> 💡 Rule: Never access `@Input` in constructor. Use `ngOnInit` or `ngOnChanges`.

### 34. How to render dynamic components using ViewContainerRef.createComponent()?

```ts
@ViewChild('container', { read: ViewContainerRef }) vcr!: ViewContainerRef;
loadComponent() {
  this.vcr.clear();
  const ref = this.vcr.createComponent(MyDynamicComponent);
  ref.instance.data = 'Hello';  // pass data to dynamic component
}
```

### 35. Create a reusable input using ControlValueAccessor.

```ts
@Component({ providers: [{ provide: NG_VALUE_ACCESSOR, useExisting: CustomInputComponent, multi: true }] })
export class CustomInputComponent implements ControlValueAccessor {
  value = '';
  onChange = (_: any) => {};
  writeValue(val: any) { this.value = val; }
  registerOnChange(fn: any) { this.onChange = fn; }
  registerOnTouched(fn: any) {}
}
```

> ✅ This lets you use the component with both `ngModel` and `FormControl`.

### 36. Custom directive using ElementRef, HostListener, Renderer2.

```ts
@Directive({ selector: '[appHighlight]' })
export class HighlightDirective {
  constructor(private el: ElementRef, private renderer: Renderer2) {}
  @HostListener('mouseenter') onEnter() {
    this.renderer.setStyle(this.el.nativeElement, 'background', 'yellow');
  }
  @HostListener('mouseleave') onLeave() {
    this.renderer.removeStyle(this.el.nativeElement, 'background');
  }
}
```

### 37. What is @HostListener and Renderer2? Why use Renderer2 instead of direct DOM manipulation?

`@HostListener` listens to events on the host element of a directive/component. **Renderer2** is an abstraction layer for DOM manipulation that works across platforms (browser, server-side rendering, Web Workers) unlike direct DOM access via `nativeElement` which breaks SSR. Use `renderer.setStyle()`, `renderer.addClass()` etc. instead of `element.style` directly.

---

## 📝 Section 5: Forms
*Q38 – Q44*

### 38. Difference between Template-driven and Reactive Forms.

| | Template-driven | Reactive Forms |
|---|---|---|
| Setup | In HTML template (ngModel) | In TypeScript (FormBuilder) |
| Validation | HTML attributes | Validator functions |
| Scalability | Simple forms | Complex/dynamic forms |
| Testing | Harder | Easier (pure TS) |
| Module | FormsModule | ReactiveFormsModule |

### 39. Difference between setValue and patchValue in Reactive Forms.

- `setValue()` — Must provide values for ALL controls. Throws error if any field is missing.
- `patchValue()` — Can provide values for a SUBSET of controls. Missing fields are unchanged.

Use `patchValue` for partial updates (e.g., pre-filling only some fields from API response).

### 40. How to create a Dynamic Form by reading from a constant/JSON config?

```ts
const formConfig = [
  { key: 'name', type: 'text', label: 'Name', required: true },
  { key: 'email', type: 'email', label: 'Email', required: true }
];
// Build form dynamically:
const group: any = {};
formConfig.forEach(f => {
  group[f.key] = ['', f.required ? Validators.required : []];
});
this.form = this.fb.group(group);
```

### 41. What is FormArray? Explain inline editing with FormArray.

`FormArray` manages a dynamic array of form controls. Used for repeatable form sections like adding multiple items.

```ts
this.form = this.fb.group({ items: this.fb.array([]) });
addItem() { (this.form.get('items') as FormArray).push(this.fb.group({ name: '', qty: 1 })); }
// Template: *ngFor="let ctrl of items.controls; let i=index"
```

### 42. How to enable the next field in a reactive form based on dropdown selection?

```ts
this.form.get('country')?.valueChanges.subscribe(value => {
  const stateCtrl = this.form.get('state');
  if (value) { stateCtrl?.enable(); }
  else { stateCtrl?.disable(); stateCtrl?.reset(); }
});
```

### 43. What is a multi-step wizard form? How to implement canDeactivate for unsaved changes?

Multi-step forms split a large form into steps using a step index. Each step has its own `FormGroup`. Navigate between steps after validating the current step. `canDeactivate` guard prevents navigation away if the form is dirty (has unsaved changes).

```ts
canDeactivate(component: MyFormComponent) {
  return component.form.dirty
    ? confirm('You have unsaved changes. Leave?')
    : true;
}
```

### 44. What is the difference between @NgModule and @Component decorators?

`@NgModule` — Configures a module: declares components/pipes/directives, imports other modules, exports things for external use, and provides services.

`@Component` — Configures a UI component: its selector, template, styles, standalone flag, and imports (in standalone mode).

With Angular 17+ standalone architecture, `@Component` can import dependencies directly, reducing reliance on `@NgModule`.

---

## 🗺️ Section 6: Routing & Guards
*Q45 – Q52*

### 45. What is routing? What is the purpose of the wildcard route?

Routing in Angular maps URL paths to components, enabling SPA navigation without page reloads. The **wildcard route** (`path: '**'`) matches any URL not defined in the routes array. Typically used as a 404 page. Must be placed last — router checks routes in order.

### 46. What are Route Guards? What types exist in Angular?

- `CanActivate` — Can user access this route?
- `CanActivateChild` — Can user access child routes?
- `CanDeactivate` — Can user leave this route? (e.g., unsaved changes)
- `CanLoad` (deprecated) / `CanMatch` — Can this lazy-loaded module be loaded?
- `Resolve` — Fetch data before route activates.

Modern Angular uses functional guards: `canActivate: [() => inject(AuthService).isLoggedIn()]`

### 47. Can we apply multiple guards on a single route? What happens if one fails?

Yes: `canActivate: [AuthGuard, RoleGuard, SubscriptionGuard]`. Guards run **sequentially** (not in parallel). If the first guard returns false or a redirect, subsequent guards are NOT executed. Navigation is cancelled at the first failing guard.

> 💡 Order matters. Put most-likely-to-fail guards first for performance.

### 48. When should we use CanActivate vs CanLoad (CanMatch)?

| | CanActivate | CanLoad / CanMatch |
|---|---|---|
| Prevents | Route activation | Lazy module loading entirely |
| Bundle download | Module still downloads | Module never downloads if false |
| Use for | Auth checks on eager routes | Truly hiding lazy modules from unauthorized users |

### 49. What does router-outlet do? Can we have more than one?

`<router-outlet>` is a placeholder where Angular renders the component matched to the current route. Yes, you can have multiple router-outlets using **named outlets**: `<router-outlet name="sidebar">`. Navigate to named outlets with: `{ outlets: { primary: ['home'], sidebar: ['menu'] } }`. Used for sidebars, popups, or multi-panel layouts.

### 50. How to implement a dynamic menu based on roles, with guards and icons/labels?

```ts
// menu.config.ts
const MENU = [
  { label: 'Dashboard', route: '/dashboard', icon: 'home', roles: ['admin','user'] },
  { label: 'Settings',  route: '/settings',  icon: 'gear', roles: ['admin'] }
];
// Filter based on user role:
visibleMenu = MENU.filter(m => m.roles.includes(this.authService.userRole));
```

### 51. How to implement permission-based / role-based directives?

```ts
@Directive({ selector: '[hasRole]' })
export class HasRoleDirective {
  @Input() set hasRole(role: string) {
    if (!this.auth.hasRole(role)) {
      this.vcr.clear();  // remove element from DOM
    }
  }
}
```
```html
<button *hasRole="'admin'">Delete</button>
```

### 52. How to implement breadcrumbs using routing as a reusable component?

Add `data: { breadcrumb: 'Home' }` to route configs. In a `BreadcrumbComponent`, subscribe to `router.events`, filter for `NavigationEnd`, then traverse `activatedRoute` snapshot building breadcrumb trail from route data.

---

## 💉 Section 7: Dependency Injection & Services
*Q53 – Q58*

### 53. Explain Dependency Injection in Angular. How does it work internally?

DI is a design pattern where a class receives its dependencies from an external source instead of creating them. Angular has a hierarchical injector tree: Root Injector → Module Injectors → Component Injectors. When a component requests a service, Angular walks up the injector tree until it finds a provider. If found at a higher level, all components sharing that injector share the same instance (singleton at that level).

### 54. Singleton services — what happens when you provide a service in a component vs lazy-loaded module?

- **Root (`providedIn: 'root'`)** — Single instance app-wide.
- **Component-level (`providers: [MyService]`)** — New instance for each component instance (and its children). Destroyed when component is destroyed.
- **Lazy-loaded module** — New child injector created; module gets its own instance if provided there, separate from root instance.

**This is a common bug source** — services intended as singletons accidentally get multiple instances.

### 55. What is providedIn in Angular?

`providedIn` in `@Injectable` specifies where to register the service.

- `'root'` — registers in the root injector (singleton, tree-shakable).
- `'platform'` — shared across multiple Angular apps on the same page.
- `'any'` — unique instance per lazy module.
- `MyModule` — registered only in that module's injector.

Most services should use `providedIn: 'root'`.

### 56. Why use NgRx/Store instead of shared services?

Shared services work well for simple state, but NgRx provides:

- **Single source of truth** — predictable state.
- **Time-travel debugging** — Redux DevTools.
- **Immutability** — reducers return new state.
- **Scalability** — clear separation of actions, reducers, effects, selectors.
- **Side-effect management** — Effects handle async operations cleanly.

Use NgRx when state is complex, shared across many components, or needs audit logging.

### 57. What is garbage collection in JavaScript?

JavaScript uses automatic garbage collection (primarily **mark-and-sweep** algorithm). The GC marks all reachable objects from roots (global scope, stack) and sweeps (frees) unreachable objects. In Angular, memory leaks occur when subscriptions keep references to components after they're destroyed — preventing GC from collecting them. Always unsubscribe in `ngOnDestroy`.

### 58. What is the ideal response time for an API? What is a CDN?

**API response time:** Ideal is under 200ms. Good is under 1s. Over 3s = poor UX. Measure with Lighthouse / Chrome DevTools Network tab.

**CDN (Content Delivery Network):** A distributed network of servers that cache static assets (JS, CSS, images) geographically close to users, reducing latency. Angular apps are deployed to CDNs for faster global delivery.

---

## 🌐 Section 8: HTTP & Interceptors
*Q59 – Q66*

### 59. What are HTTP Interceptors? Use cases?

Interceptors intercept every outgoing HTTP request and incoming response, allowing cross-cutting concerns to be handled in one place.

- **Token attachment** — Add Authorization header to every request.
- **Global error handling** — Handle 401/403/500 errors centrally.
- **Loading spinner** — Show/hide loader on request/response.
- **Caching** — Return cached responses.
- **Request logging / profiling** — Log API timings.
- **Mocking** — Return fake data in development/testing.

### 60. Write interceptor code for attaching token and handling errors.

```ts
export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const token = inject(AuthService).getToken();
  const authReq = token
    ? req.clone({ setHeaders: { Authorization: `Bearer ${token}` } })
    : req;
  return next(authReq).pipe(
    catchError(err => {
      if (err.status === 401) inject(Router).navigate(['/login']);
      return throwError(() => err);
    })
  );
};
```

### 61. Can we have multiple interceptors? What is their order?

Yes. Register multiple interceptors in `providers`. They execute in the **order registered for requests**, and in **reverse order for responses** (like middleware stack). Angular 17+ functional interceptors: `withInterceptors([loggingInterceptor, authInterceptor])`. The request goes: logging → auth → server. Response comes back: auth → logging.

### 62. How do you call multiple APIs simultaneously in Angular?

```ts
// forkJoin — wait for ALL to complete
forkJoin([this.api.getUsers(), this.api.getOrders()])
  .subscribe(([users, orders]) => { ... });

// combineLatest — emit when ANY changes
combineLatest([user$, settings$]).subscribe(([user, settings]) => {...});

// Promise.race equivalent — first to respond wins
race([api1$, api2$]).subscribe(firstResult => {...});
```

### 63. How to call an API only after the previous one completes?

```ts
// switchMap / concatMap for sequential calls
this.api.getUser(id).pipe(
  switchMap(user => this.api.getOrdersForUser(user.id))
).subscribe(orders => {...});

// concatMap if order matters and no cancellation needed
requests$.pipe(concatMap(req => this.api.process(req))).subscribe();
```

### 64. Difference between forkJoin vs mergeMap?

- `forkJoin` — Combines multiple observables, waits for ALL to complete, emits one combined result. Best for parallel independent API calls where you need all results.
- `mergeMap` (flatMap) — Maps each emission to an inner observable and merges their outputs concurrently without waiting. Best for parallel operations where each input triggers a separate async operation (e.g., uploading multiple files simultaneously).

### 65. What is the difference between package.json and package-lock.json?

`package.json` — Declares project dependencies with version ranges (e.g., `^17.0.0`). Human-editable.

`package-lock.json` — Records the exact version tree of every installed package. Auto-generated by npm. Ensures reproducible installs across machines — same exact versions are installed every time. Always commit `package-lock.json` to version control.

### 66. How to prevent duplicate form submissions when API is slow?

```ts
// Use exhaustMap — ignores new clicks while request is in-flight
this.submitBtn.clicks$.pipe(
  exhaustMap(() => this.api.submit(this.form.value))
).subscribe();

// OR: disable button on submit, re-enable on response
isSubmitting = false;
onSubmit() { this.isSubmitting = true; this.api.submit()
  .pipe(finalize(() => this.isSubmitting = false)).subscribe(); }
```

---

## 🔃 Section 9: RxJS & Observables
*Q67 – Q74*

### 67. Observable vs Promise — key differences?

| | Observable | Promise |
|---|---|---|
| Values | Multiple values over time (stream) | Single value |
| Lazy | Yes — executes only when subscribed | No — executes immediately |
| Cancellable | Yes — `unsubscribe()` | No |
| Operators | Rich (map, filter, switchMap...) | Limited (.then, .catch) |
| Use for | HTTP streams, events, WebSocket | Single async operations |

### 68. Cold vs Hot Observables? Unicast vs Multicast?

- **Cold Observable** — Creates a new producer for each subscriber (unicast). E.g., HTTP request — each subscribe triggers a new HTTP call.
- **Hot Observable** — Shares a single producer across all subscribers (multicast). E.g., mouse events, WebSocket — subscribers receive values happening at the time of subscription.

**Subjects** are hot and multicast. Use `share()` or `publish()` to make cold observables hot.

### 69. Subject vs BehaviorSubject vs ReplaySubject?

| | Subject | BehaviorSubject | ReplaySubject |
|---|---|---|---|
| Initial value | None | Required | None |
| New subscriber gets | Only future values | Current + future values | Last N values + future |
| Use for | Events | State (current value matters) | History needed |

### 70. Explain switchMap, mergeMap, concatMap, exhaustMap with real scenarios.

| Operator | Behavior | Real-world use case |
|---|---|---|
| `switchMap` | Cancels previous inner observable | Search autocomplete (cancel old search on new input) |
| `mergeMap` | Runs all concurrently | Parallel file uploads |
| `concatMap` | Queues — waits for previous to complete | Sequential API calls, ordered uploads |
| `exhaustMap` | Ignores new while current runs | Login/submit button — prevent duplicate submissions |

### 71. How to avoid memory leaks in Angular? (unsubscribe, takeUntil, async pipe)

```ts
// Option 1: takeUntilDestroyed (Angular 16+) — RECOMMENDED
data$ = this.api.getData().pipe(takeUntilDestroyed());

// Option 2: async pipe — auto unsubscribes
// Template: <div *ngIf="data$ | async as data">

// Option 3: manual takeUntil
destroy$ = new Subject<void>();
this.data$.pipe(takeUntil(this.destroy$)).subscribe();
ngOnDestroy() { this.destroy$.next(); this.destroy$.complete(); }
```

### 72. What are Promises? Explain Promise.all, Promise.race, Promise.allSettled.

- `Promise.all([p1,p2,p3])` — Resolves when ALL resolve. Rejects immediately if ANY reject.
- `Promise.race([p1,p2,p3])` — Settles with the FIRST to settle (resolve or reject).
- `Promise.allSettled([p1,p2,p3])` — Waits for ALL to settle regardless of resolve/reject; returns array of `{status, value/reason}`.
- `Promise.any([p1,p2,p3])` — Resolves with first to resolve; rejects only if ALL reject.

### 73. What is async/await? How does it differ from Promises?

async/await is syntactic sugar over Promises, making async code read like synchronous code. `async` marks a function as returning a Promise. `await` pauses execution inside that function until the Promise resolves. Under the hood it's still Promises — the difference is readability and error handling (`try/catch` instead of `.catch()`).

```ts
async fetchData() {
  try {
    const user = await this.api.getUser();
    const orders = await this.api.getOrders(user.id);
  } catch(err) { console.error(err); }
}
```

### 74. RxJS tap operator — when to use it?

`tap()` performs side effects without modifying the stream. Use it for: logging, debugging, triggering UI state changes (show loader), or tracking analytics — without disrupting the data flow through the pipe.

```ts
this.api.getUsers().pipe(
  tap(() => this.loading = true),
  tap(data => console.log('Debug:', data))
).subscribe();
```

---

## 🏪 Section 10: State Management & NgRx
*Q75 – Q80*

### 75. What are NgRx actions, reducers, effects, and selectors?

- **Actions** — Plain objects describing events: `createAction('[Users] Load')`.
- **Reducers** — Pure functions that take state + action and return new state.
- **Effects** — Handle side effects (API calls); listen for actions, perform async work, dispatch new actions.
- **Selectors** — Memoized functions to query/derive state: `createSelector()`.
- **Store** — Single immutable state tree (Observable).

**Flow:** Component dispatches action → Effect handles async → dispatches success/fail action → Reducer updates state → Selector reads state → Component receives update.

### 76. Subject vs BehaviorSubject — when to use which? (Scenario-based)

- **Use Subject** when: You only care about future values after subscription (button clicks, event bus).
- **Use BehaviorSubject** when: New subscribers need the current/last value immediately (user auth state, theme, cart items — any state that new components need on initialization).

```ts
// Auth service example
isLoggedIn$ = new BehaviorSubject<boolean>(false);
// Any component that subscribes later still gets current login state
```

### 77. Real use cases for forkJoin?

forkJoin is perfect when you need to load multiple independent data sources before rendering a page:

```ts
forkJoin({
  user: this.api.getUser(id),
  roles: this.api.getRoles(),
  settings: this.api.getSettings()
}).subscribe(({ user, roles, settings }) => {
  this.vm = { user, roles, settings }; // render all at once
});
```

### 78. How do you handle persist filter state when navigating back to a page?

Options:

1. **Query params** — Store filters in URL `?from=2024&category=sales` — shareable, browser-back works.
2. **Service / Store** — Keep filter state in a singleton service or NgRx store.
3. **SessionStorage** — Persist within tab session.
4. **Router state** — Pass state via router extras `{ state: { filters } }`.

URL query params is the most robust and user-friendly approach.

### 79. How do you keep a user logged in even if the browser tab is closed?

Store the auth token in **localStorage** (persists across sessions, survives tab close) instead of sessionStorage (clears on tab close). On app startup, check localStorage for an existing valid token and auto-login the user. Implement refresh token rotation — store refresh token in an HttpOnly cookie (more secure) and access token in memory or localStorage.

### 80. RxJS Schedulers — what are they?

Schedulers control when and in what context RxJS work executes.

- `asyncScheduler` — like `setTimeout`, runs asynchronously.
- `animationFrameScheduler` — runs before browser repaint (smooth animations).
- `queueScheduler` — runs synchronously in a queue.
- `asapScheduler` — runs asap after current sync code (microtask).

Use with `observeOn(asyncScheduler)` or `subscribeOn()`. Most commonly asked in senior interviews for performance-critical code.

---

## ⚡ Section 11: Performance Optimization
*Q81 – Q86*

### 81. Angular performance optimization techniques?

- Use **OnPush** Change Detection + immutable data patterns
- **Lazy loading** modules and components
- **TrackBy** in `*ngFor` / `@for` to minimize DOM re-renders
- **Deferrable views** (`@defer`) for below-the-fold content
- **Pure pipes** instead of methods in templates
- **Virtual scrolling** (CDK) for large lists
- **Server-Side Rendering** (Angular Universal) for faster FCP
- **Image optimization** — `NgOptimizedImage` directive
- **Preloading strategies** — `PreloadAllModules` or custom
- **Signals** for zoneless reactivity

### 82. How do you identify performance bottlenecks? What tools to use?

- **Lighthouse** (Chrome DevTools) — Audit LCP (Largest Contentful Paint), FCP (First Contentful Paint), TTI (Time to Interactive), CLS.
- **Chrome DevTools Performance tab** — Record and analyze JS execution.
- **Angular DevTools** — Visualize component tree, CD cycles, profiling.
- **webpack-bundle-analyzer** — Visualize bundle sizes.
- **Source Maps + Network tab** — Identify large bundles.

Target: LCP < 2.5s, FCP < 1.8s.

### 83. What is TrackBy in ngFor and @for? Why is it important?

Without trackBy, Angular re-renders the entire DOM list on any data change (even if only one item changed). With trackBy, Angular identifies items by a unique key and only re-renders changed items.

```html
<!-- Old: *ngFor -->
*ngFor="let item of items; trackBy: trackById"
trackById(index: number, item: Item) { return item.id; }

<!-- New: @for (Angular 17+) — trackBy is required! -->
@for (item of items; track item.id) { <div>{{ item.name }}</div> }
```

### 84. Virtual scrolling for large lists — how to implement?

Angular CDK's `ScrollingModule` renders only visible items, dramatically improving performance for lists with thousands of rows.

```html
<cdk-virtual-scroll-viewport itemSize="50" style="height:400px">
  <div *cdkVirtualFor="let item of items">{{ item.name }}</div>
</cdk-virtual-scroll-viewport>
```

> ✅ For external libraries: CDK Virtual Scroll, AG Grid (built-in), or PrimeNG VirtualScroller

### 85. How to handle large data using API-based pagination?

```ts
getPage(page: number, size: number) {
  return this.http.get<PagedResult>(`/api/data?page=${page}&size=${size}`);
}
// Infinite scroll: use IntersectionObserver to detect bottom
// Server-side sort/filter: send params to API instead of filtering locally
```

### 86. What are the bottleneck investigation steps for a slow Angular application?

1. **Run Lighthouse** — identify LCP, FCP, JS parse time.
2. **Angular DevTools Profiler** — find components with excessive CD cycles.
3. **Bundle analyzer** — check for large/duplicate packages.
4. **Network tab** — waterfall analysis, slow APIs.
5. **Check `*ngFor` without trackBy** — list re-renders.
6. **Check for OnPush opportunities**.
7. **Check template methods** — replace with pure pipes.
8. **Lazy load heavy features**.

---

## 🏛️ Section 12: Angular Architecture & Advanced
*Q87 – Q96*

### 87. What is Micro Frontend architecture and Module Federation?

Micro Frontend splits a large frontend app into independently deployable pieces (by team/domain). Each team builds and deploys their part independently. **Module Federation** (webpack 5) is the primary technology enabling this in Angular — it allows one Angular app (shell) to dynamically load components/modules from other apps (remotes) at runtime. Use `@angular-architects/module-federation` for Angular-specific setup. Solves large-team coordination and independent deployment problems.

### 88. Angular Universal vs SSR — what's the difference?

**Angular Universal** — The original server-side rendering solution for Angular (runs on Node.js/Express). Renders HTML on server and sends to browser.

**SSR in Angular 17+** — Angular has dramatically improved built-in SSR with `ng add @angular/ssr`, non-destructive hydration, and partial hydration. Hydration merges server-rendered HTML with client Angular without re-rendering.

**Benefits:** Faster FCP/LCP, better SEO, improved performance on low-end devices.

### 89. Angular migration from Angular 12/16 to newer versions — what steps to follow?

1. Use **ng update**: `ng update @angular/core@17 @angular/cli@17`.
2. Fix breaking changes from migration guide (angular.io/guide/update).
3. Update RxJS, TypeScript, and third-party packages.
4. Run `ng update --migrate-only` to apply code migrations.
5. Test thoroughly in a branch.
6. Migrate incrementally (one major version at a time).
7. Optional: Convert to standalone architecture with `ng generate @angular/core:standalone`.

### 90. In standalone architecture, is zone.js still required?

Not required but included by default. With Angular 18+, you can opt into a **zoneless** application by providing:

```ts
bootstrapApplication(AppComponent, { providers: [provideExperimentalZonelessChangeDetection()] })
```

This requires using Signals for all reactivity — no zone.js to trigger CD. The Angular team is working toward making this the default in future versions.

### 91. What is CI/CD pipeline? How to manage different environment builds (dev/QA/prod)?

**CI/CD** — Continuous Integration (automated build + test) / Continuous Deployment (automated deploy). Angular uses environment files: `environment.ts` (dev), `environment.qa.ts`, `environment.prod.ts`. Configure in `angular.json` fileReplacements. Build with: `ng build --configuration=qa`. CI/CD tools: GitHub Actions, Jenkins, Azure DevOps. Pipeline: Code push → Build → Test → Deploy to env.

### 92. What is Internationalization (i18n) in Angular?

Angular has built-in i18n support. Mark text with `i18n` attribute: `<h1 i18n>Hello</h1>`. Extract with `ng extract-i18n` (creates XLIFF/JSON files). Provide translations per locale. Build with `ng build --localize` to create locale-specific bundles. Alternative: `ngx-translate` library for runtime translation switching.

### 93. What is the difference between AngularJS and Angular (2+)?

| | AngularJS (1.x) | Angular (2+) |
|---|---|---|
| Language | JavaScript | TypeScript |
| Architecture | MVC / $scope based | Component-based |
| Data binding | Two-way by default | One-way (explicit two-way) |
| DI | Strings-based | Type-based hierarchy |
| Mobile | Not mobile-friendly | Mobile-first, PWA support |

### 94. Project uses PrimeNG but needs migration to Angular Material — how will you plan and manage branching without affecting sprints?

1. Create a **feature branch** (e.g., `feat/material-migration`).
2. Implement a **component-by-component migration** strategy — create wrapper components that use Angular Material internally.
3. Use **feature flags** to toggle between old/new components.
4. Migrate low-risk components first (buttons, inputs).
5. Keep main branch clean — merge only completed, tested components.
6. Never break the sprint — migrate alongside feature work.

### 95. Polling / auto-refresh / auto-save in Angular?

```ts
// Polling with RxJS interval
interval(5000).pipe(
  startWith(0),
  switchMap(() => this.api.getData()),
  takeUntilDestroyed()
).subscribe(data => this.data = data);

// Auto-save with debounce on form changes
this.form.valueChanges.pipe(
  debounceTime(2000),
  switchMap(val => this.api.autosave(val))
).subscribe();
```

### 96. How does Angular bootstrapping work?

Angular starts via `main.ts`. Classic: `platformBrowserDynamic().bootstrapModule(AppModule)` — compiles and bootstraps AppModule. Modern (standalone): `bootstrapApplication(AppComponent, { providers: [...] })` — no module needed. Angular then: compiles components (AOT = already done at build time), renders the root component into `<app-root>` in index.html, starts change detection and routing.

---

## 🔐 Section 13: Authentication & Security
*Q97 – Q100*

### 97. Explain the full JWT authentication flow in Angular.

1. User submits login form → Angular sends credentials to auth API.
2. Server validates → returns **JWT access token** + **refresh token**.
3. Angular stores access token (localStorage/memory) and refresh token (HttpOnly cookie or localStorage).
4. HTTP Interceptor attaches: `Authorization: Bearer {token}` to all API requests.
5. Server validates JWT signature and expiry.
6. On 401 (expired) → Interceptor calls refresh endpoint → gets new access token → retries original request.
7. Logout → clear tokens + call revoke endpoint.

### 98. OAuth 2.0 and Auth0 integration in Angular?

OAuth 2.0 is an authorization framework — delegates authentication to an identity provider (Google, Azure AD, Auth0). Angular uses the **Authorization Code Flow with PKCE** for SPAs. With Auth0: install `@auth0/auth0-angular`, configure in AppModule/providers with domain and clientId. `AuthModule` provides guards and HTTP interceptor for automatic token attachment. `AuthService` provides login/logout/user profile methods.

### 99. How to handle token expiry and refresh token rotation?

```ts
// In HTTP Interceptor — handle 401 with token refresh
catchError(err => {
  if (err.status === 401 && !req.url.includes('refresh')) {
    return this.auth.refreshToken().pipe(
      switchMap(tokens => {
        this.auth.saveTokens(tokens);
        return next(req.clone({setHeaders:{Authorization:`Bearer ${tokens.access}`}}));
      })
    );
  }
  return throwError(() => err);
})
```

### 100. Role-based access control — multiple roles for one route?

```ts
// Route with role data
{ path: 'reports', component: ReportsComponent,
  data: { roles: ['admin', 'manager'] },
  canActivate: [RoleGuard] }

// RoleGuard checks user role against route data
const allowedRoles = route.data['roles'] as string[];
return allowedRoles.includes(this.auth.currentUserRole);
```

---

## 💛 Section 14: JavaScript Fundamentals
*Q101 – Q114*

### 101. What is closure in JavaScript? Where does it accidentally cause bugs?

A closure is a function that has access to its outer scope's variables even after the outer function has returned. The inner function "closes over" those variables.

```js
function counter() {
  let count = 0;
  return () => ++count; // closes over count
}
// Bug: var in loops — all closures share same variable
for (var i = 0; i < 3; i++) { setTimeout(() => console.log(i), 100); }
// Prints 3,3,3 — use let or IIFE to fix
```

### 102. What is hoisting? What is the Temporal Dead Zone (TDZ)?

**Hoisting** — JavaScript moves declarations (not initializations) to the top of their scope. `var` declarations are hoisted and initialized as `undefined`. `function` declarations are fully hoisted. `let` and `const` are hoisted but NOT initialized.

**TDZ (Temporal Dead Zone)** — The period between the start of a block scope and the declaration of a let/const variable. Accessing the variable in TDZ throws a `ReferenceError`.

### 103. Difference between var, let, and const?

| | var | let | const |
|---|---|---|---|
| Scope | Function | Block | Block |
| Hoisting | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Re-declare | Yes | No | No |
| Re-assign | Yes | Yes | No |
| Use today | Avoid | For changing values | Preferred (default) |

### 104. Difference between Arrow Functions and Normal Functions?

- **this binding** — Arrow functions inherit `this` from lexical scope (no own this). Normal functions have their own `this` based on how called.
- **No own arguments** — Arrow functions have no `arguments` object.
- **Cannot be constructor** — Arrow functions can't be used with `new`.
- **No prototype** — Arrow functions lack a prototype property.

In Angular, always use arrow functions in callbacks to preserve component `this`.

### 105. What is event bubbling, capturing, and event delegation?

- **Bubbling** — Event fires on target, then bubbles up through ancestors. Default behavior.
- **Capturing** — Event travels from root down to target (`useCapture: true`).
- **Event Delegation** — Instead of attaching handlers to many child elements, attach ONE handler to a parent and use `event.target` to identify the source. Improves performance and handles dynamically added elements.

```js
parentEl.addEventListener('click', e => {
  if (e.target.matches('.item')) { handleItemClick(e); }
});
```

### 106. What is the Event Loop? Explain microtasks vs macrotasks.

The event loop enables JavaScript's non-blocking async behavior on a single thread.

- **Call Stack** — Executes sync code.
- **Macrotask queue** (task queue) — setTimeout, setInterval, I/O events.
- **Microtask queue** — Promise.then, queueMicrotask, MutationObserver.

**Order:** All sync code runs → All microtasks drain → ONE macrotask runs → All microtasks drain → Next macrotask. Microtasks always run before the next macrotask.

### 107. What are pure functions? Have you used them in Angular?

A pure function: (1) Given the same inputs, always returns the same output. (2) Has no side effects (no external state modification).

In Angular: **NgRx reducers** must be pure functions. **Pure pipes** rely on pure-function semantics. Using pure functions with immutable data makes OnPush change detection work correctly and makes code predictable and testable.

### 108. What is prototypal inheritance in JavaScript?

Every JavaScript object has an internal `[[Prototype]]` link to another object (its prototype). When accessing a property, JS looks on the object first, then walks up the prototype chain until found or reaching null. `class` syntax is syntactic sugar over prototypal inheritance. Constructor functions create the prototype chain. TypeScript's class inheritance compiles to prototype-based code.

### 109. What is currying / infinite currying? Explain with use cases.

```js
// Currying: transform f(a,b,c) into f(a)(b)(c)
const add = a => b => a + b;
add(5)(3); // 8

// Infinite currying:
const sum = a => b => b ? sum(a + b) : a;
sum(1)(2)(3)(); // 6

// Use case: reusable, partially-applied functions
const multiply = x => y => x * y;
const double = multiply(2);  // partial application
[1,2,3].map(double);          // [2,4,6]
```

### 110. Spread vs Rest operator? Destructuring?

```js
// Spread — expand iterable
const merged = [...arr1, ...arr2];  // arrays
const newObj = { ...obj, extra: 1 }; // objects (immutable update)

// Rest — collect remaining
function sum(...nums) { return nums.reduce((a,b) => a+b, 0); }

// Destructuring
const { name, age = 25 } = user;   // object with default
const [first, , third] = arr;      // array skip element
```

### 111. Why does 0.1 + 0.2 !== 0.3?

JavaScript uses IEEE 754 double-precision floating-point numbers. Some decimal fractions (like 0.1 and 0.2) can't be represented exactly in binary floating-point — they become repeating fractions. When added, the tiny imprecision compounds: `0.1 + 0.2 = 0.30000000000000004`. Fix: Use `Number((0.1 + 0.2).toFixed(2))`, multiply to integers for calculation, or use a library like decimal.js for financial calculations.

### 112. Generator function output — explain with example.

```js
function* add() {
  yield 1;         // 1st call: {value:1, done:false}
  yield [2,3];     // 2nd call: {value:[2,3], done:false}
  return 4;        // 3rd call: {value:4, done:true}
}                  // 4th call: {value:undefined, done:true}

const gen = add();
gen.next(); // {value:1, done:false}
gen.next(); // {value:[2,3], done:false}
gen.next(); // {value:4, done:true}
gen.next(); // {value:undefined, done:true}
```

### 113. Difference between slice and splice?

| | slice(start, end) | splice(start, deleteCount, ...items) |
|---|---|---|
| Mutates original? | No (returns new array) | Yes (modifies in place) |
| Returns | New sub-array | Array of removed elements |
| Can insert? | No | Yes |
| Use for | Copying / extracting | Removing/inserting elements |

### 114. Variable shadowing in JavaScript?

```js
const x = 10;  // outer x
function test() {
  const x = 20;        // shadows outer x
  console.log(x);     // 20 — inner x wins
}
console.log(x);  // 10 — outer unaffected
// Shadowing with let vs var can cause subtle bugs in loops
```

---

## 💻 Section 15: TypeScript & Coding Challenges
*Q115 – Q128*

### 115. Difference between any and unknown in TypeScript? What about generics?

- `any` — Opts out of type checking entirely. Any operation is allowed — unsafe.
- `unknown` — Type-safe counterpart. You must perform type checks before using the value.
- **Generics** — Type variables that make functions/classes reusable across types while preserving type safety: `function identity<T>(arg: T): T { return arg; }`.

Variance in TS: Covariance (subtype is assignable), Contravariance (params), Invariance (mutable generics).

### 116. TypeScript Interfaces, optional properties, Partial<T>?

```ts
interface User {
  id: number;
  name: string;
  email?: string;  // optional
}
// Utility types:
type PartialUser = Partial<User>;    // all props optional
type ReadonlyUser = Readonly<User>;  // all props readonly
type PickUser = Pick<User, 'id'|'name'>; // subset
type OmitEmail = Omit<User, 'email'>; // exclude field
```

### 117. parseInt('08', 10) vs parseInt('08') — what is the output?

```js
parseInt('08')     // 8 (modern JS — defaults to decimal)
parseInt('08', 10)  // 8 (explicit base 10 — always safe)
parseInt('08', 8)   // 0 (octal — '8' is invalid in base 8)
parseInt('010')    // 10 (modern), was 8 in older engines
// Best practice: always pass radix as second argument!
```

### 118. Write code to find missing numbers from an array like [1,2,4,5,7,8,9]?

```ts
function findMissing(arr: number[]) {
  const max = Math.max(...arr);
  const set = new Set(arr);
  const missing = [];
  for (let i = 1; i <= max; i++) {
    if (!set.has(i)) missing.push(i);
  }
  return missing;  // [3, 6]
}
```

### 119. Find duplicate values in a string like "program"?

```ts
function findDuplicates(str: string) {
  const freq: Record<string, number> = {};
  for (const ch of str) freq[ch] = (freq[ch] || 0) + 1;
  return Object.entries(freq)
    .filter(([_, count]) => count > 1)
    .map(([ch]) => ch);
}
findDuplicates('program'); // ['r', 'g'] (r×2, g×2)
```

### 120. Flatten a nested array: [1, [2, [3, [4]], 5]] → [1, 2, 3, 4, 5]?

```ts
// Method 1: flat() with Infinity depth
[1, [2, [3, [4]], 5]].flat(Infinity);  // [1,2,3,4,5]

// Method 2: Recursive
function flatten(arr: any[]): any[] {
  return arr.reduce((flat, item) =>
    flat.concat(Array.isArray(item) ? flatten(item) : item), []);
}
```

### 121. Remove duplicate objects from array by combination of empId and name?

```ts
const employees = [
  { empId: 1, name: 'Alice', city: 'NY' },
  { empId: 1, name: 'Alice', city: 'LA' },  // duplicate
  { empId: 2, name: 'Bob', city: 'NY' }
];
const unique = [...new Map(
  employees.map(e => [`${e.empId}_${e.name}`, e])
).values()];
// Result: [{empId:1,name:'Alice',city:'NY'}, {empId:2,...}]
```

### 122. Chunk an array into fixed sizes: [42,10,19,6,8,7] with size 3?

```ts
function chunk<T>(arr: T[], size: number): T[][] {
  const result: T[][] = [];
  for (let i = 0; i < arr.length; i += size) {
    result.push(arr.slice(i, i + size));
  }
  return result;
}
chunk([42,10,19,6,8,7], 3); // [[42,10,19],[6,8,7]]
```

### 123. Replace repeated values with 1: [1,2,3,2,3,4] → [1,1,1,1,1,4]?

```ts
function replaceRepeated(arr: number[]) {
  const seen = new Set<number>();
  return arr.map(n => {
    if (seen.has(n)) return 1;
    seen.add(n);
    return n;
  });
}
replaceRepeated([1,2,3,2,3,4]); // [1,2,3,1,1,4]
```

### 124. Find the second highest salary using SQL CTE?

```sql
-- Using CTE (Common Table Expression)
WITH RankedSalaries AS (
  SELECT Salary,
         DENSE_RANK() OVER (ORDER BY Salary DESC) AS Rank
  FROM Employees
)
SELECT Salary FROM RankedSalaries WHERE Rank = 2;
-- CTE = temporary named result set, readable alternative to subqueries
```

### 125. Prototype chain question: delete x.p — what does console.log(x.p) print?

```js
function A() {}
A.prototype.p = 1;       // prototype property p = 1
const x = new A();
x.p = 2;                 // own property p = 2 (shadows prototype)
delete x.p;             // deletes OWN property only
console.log(x.p);        // 1 (falls back to prototype.p)
delete A.prototype.p;   // deletes prototype property
console.log(x.p);        // undefined (no more prototype.p)
```

### 126. Write code for method overriding in TypeScript (OOP)?

```ts
class Animal {
  speak() { return 'Some sound'; }
}
class Dog extends Animal {
  override speak() {   // override keyword (TS 4.3+)
    return 'Woof!';     // overrides parent method
  }
}
const d = new Dog();
d.speak();  // 'Woof!'
super.speak(); // access parent: 'Some sound'
```

### 127. Difference between WHERE and HAVING in SQL?

| | WHERE | HAVING |
|---|---|---|
| Filters | Individual rows (before grouping) | Groups (after GROUP BY) |
| Use with aggregates | No | Yes (SUM, COUNT, AVG...) |
| Example | `WHERE salary > 50000` | `HAVING COUNT(*) > 5` |

### 128. Git commands: create branch, switch branch, cherry-pick?

```bash
# Create and switch to new branch
git checkout -b feature/my-feature
git switch -c feature/my-feature   # modern syntax

# Switch to existing branch
git checkout main
git switch main

# Cherry-pick: apply a specific commit from another branch
git cherry-pick <commit-hash>
# Useful for: hotfix on main, backporting a specific fix
```

---

## 👨‍💻 About

**Code With Krishna** — Angular Developer · Interview Preparation Enthusiast

[LinkedIn Profile](https://www.linkedin.com/in/codewithkrishnax) · [GitHub](https://github.com/codewithkrishnax)

**128** Unique Questions · **15** Topic Areas · Angular 17–20 · MNC Interview Ready

This guide was compiled from 20+ real MNC interview experience posts shared on LinkedIn by developers who interviewed at Tech Mahindra, LTIMindtree, and other top Indian MNCs. Questions were extracted, deduplicated, categorized, and answered for comprehensive interview preparation. All questions are unique — no repetitions.

📌 **Topics:** Angular Core · Change Detection · Signals · RxJS · NgRx · Forms · Routing · DI · HTTP Interceptors · Auth · Performance · JS Fundamentals · TypeScript

*Angular Interview Questions Guide · 2025 Edition · Curated with ❤️ by Code With Krishna*
