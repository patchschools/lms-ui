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
```
<header>
    <nav class="navbar navbar-expand-sm fixed-top" style="background-color: rgb(43, 54, 67);">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">YourProduct</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarID" aria-controls="navbarID" aria-expanded="false" aria-label="Toggle navigation">
              <span class="navbar-toggler-icon"></span>
          </button>
        </div>
        <div class="collapse navbar-collapse" id="navbarID">


            <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
                <li class="nav-item">
                    <a class="nav-link active" aria-current="page" routerLink="/home" [routerLinkActive]="['active']" [routerLinkActiveOptions]="{exact:true}"> Home</a>
                </li>


                <!--
                <ng-template #notloggedin>

                </ng-template> -->
            </ul>

            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <ng-container *ngIf="(user | async) let userDetail else notloggedin">


                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page">{{userDetail.name}}</a>
                    </li>

                    <li class="nav-item">
                        <a class="nav-link" aria-current="page" (click)="logout()">Logout</a>
                    </li>


                </ng-container>
                <ng-template #notloggedin>
                    <li class="nav-item">
                        <a class="nav-link" aria-current="page" routerLink="/auth/login">Login</a>
                    </li>

                    <li class="nav-item">
                        <a class="nav-link" aria-current="page" routerLink="/auth/register">Register</a>
                    </li>
                </ng-template>

            </ul>


        </div>

    </nav>
</header>
```

```
import { AuthService } from './../../auth/auth.service';
import { Observable } from 'rxjs';
import { Component, Input, OnInit } from '@angular/core';
import { User } from 'src/app/model/user';
import { Router } from '@angular/router';

@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
  styles: [
  ]
})
export class HeaderComponent implements OnInit {

  @Input()
  user:Observable<User>;

  constructor(private authService :AuthService,private router:Router) {
    this.user = this.authService.loginSubject;
   }

  ngOnInit(): void {
  }

  logout(){
    this.authService.logout();
    this.router.navigateByUrl("home");
  }


}

```

##### Step 2.4: Create Sidebar
```
ng g c sidebar
```

```
<aside class="sidebar">

    <ul class="nav sidebar-menu">
        <li class="nav-item" *ngFor="let m of menus">
            <a routerLink="/{{m.path}}" class=" nav-link " [routerLinkActive]="['active']" [routerLinkActiveOptions]="{exact:true}">

                <span class=" ">{{m.name}}</span>
            </a>
        </li>
    </ul>
</aside>
```


```
import { Component, Input, OnInit } from '@angular/core';
import { FormGroup, FormBuilder } from '@angular/forms';

@Component({
  selector: 'app-sidebar',
  templateUrl: './sidebar.component.html',
  styles: [
  ]
})
export class SidebarComponent implements OnInit {

  options: FormGroup;

  @Input()
  menus:any;

  constructor(fb: FormBuilder) {
    this.options = fb.group({
      bottom: 0,
      fixed: false,
      top: 0
    });
  }

  ngOnInit(): void {
  }

}

```

##### Step 2.5: Create Menu
```
ng g class menu
```

