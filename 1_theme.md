## Build a Theme

##### Step 1: Create Theme Library

```
ng g lib kt-theme --prefix=kt
```

##### Step 2: Create Layout Module 

```
ng g m layout
```

##### Step 2.1: Create Admin Layout Components
```
ng g c adminLayout
```

```
<router-outlet></router-outlet>
```

##### Step 2.2: Create Auth Layout Component
```
ng g c authLayout
```
```
<div class="wrapper">
    <div class="page">

        <router-outlet></router-outlet>

    </div>
</div>
```

##### Step 2.3: Create Header
```
ng g c header
```

##### Step 2.4: Create Sidebar
```
ng g c sidebar
```

##### Step 2.5: Create Menu
```
ng g class menu
```

