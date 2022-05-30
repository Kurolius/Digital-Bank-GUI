# Digital Banking GUI

This is a Web application based on Angular consuming this [REST API](https://github.com/Kurolius/Digital-Bank-API) and the two form a digital banking project

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 13.3.7.

## Development server

Run `ng serve` 

## Project structur
![image](https://user-images.githubusercontent.com/84138772/171067157-2c89ef4a-a76d-4eb8-b37b-07d05dae59e0.png)

## Models
### User
```TypeScript
export interface User{
    id: string,
    username: string,
    roles: [
        {
            roleName: string
        }
    ]
}
```
### Customer
```TypeScript
export interface Customer {
    id: string;
    name: string;
    email: string;
} 

export interface CustomersPaginated {
    currentPage :number,
    totalPages :number,
    pageSize :number,
    customers :Customer[]
}
```
### Account
```TypeScript
import { Customer } from "./customer.model";


export interface BankAccount {
    type: string;
    id: string;
    balance: number;
    createdAt: Date;
    customer: Customer;
    status: string;
    interestRate?: number;
    overDraft?: number;
}

export interface CustomerAccountResponse {
    customerId: string;
    currentPage: number;
    totalPages: number;
    pageSize: number;
    accounts: BankAccount[];
}
```
### Operation
```TypeScript
export interface Operation {
    id: number;
    operationDate: Date;
    amount: number;
    type: string;
    description: string;
}

export interface OperationResponseObject {
    accountId: string;
    balance: number;
    currentPage: number;
    totalPages: number;
    pageSize: number;
    accountOperationDTOS: Operation[];
}
```
## Routing

```TypeScript
const routes: Routes = [
  {
    path: "",
    loadChildren: ()=>import("./pages/home/home.module").then(e=>e.HomeModule)
  },
  {
    path: "accounts",
    loadChildren: ()=>import("./pages/accounts/accounts.module").then(e=>e.AccountsModule),
    canActivate: [ UserGuardGuard]
  },
  {
    path: "customers",
    loadChildren: ()=>import("./pages/customers/customers.module").then(e=>e.CustomersModule),
    canActivate: [ UserGuardGuard]
  },
  {
    path: "operations",
    loadChildren: ()=>import("./pages/operations/operations.module").then(e=>e.OperationsModule),
    canActivate: [ UserGuardGuard]
  },
  {
    path: "login",
    component: LoginComponent,
    canActivate: [GuestGuardGuard]
  },
  {
    path: "**",
    component: Error404Component  
  }
];
```
## Overview :

- Home page :
![image](https://user-images.githubusercontent.com/84138772/171067534-9255171c-a7fd-4a4e-959d-1d08b05fd0a6.png)

- Login page :
![image](https://user-images.githubusercontent.com/84138772/171067573-5027db06-5c22-4c26-b4b4-e1e78afab8d7.png)

- List of costumers page :
![image](https://user-images.githubusercontent.com/84138772/171067638-6b50e97a-7a8c-404d-85f3-7a828001ac17.png)

- Add new customer page :
![image](https://user-images.githubusercontent.com/84138772/171067661-654afba2-6318-4aa4-98f2-d8e0e3190abb.png)

- Accounts page :
![image](https://user-images.githubusercontent.com/84138772/171067715-a3f26fa7-e8ac-46cc-8693-768520dbf7d9.png)

- Operation page :
![image](https://user-images.githubusercontent.com/84138772/171067763-9c617062-e613-45cc-be5e-c4a7ca35b5b1.png)
