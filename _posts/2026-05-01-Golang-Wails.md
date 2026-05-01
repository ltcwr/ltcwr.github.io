---
title: "How to create a Desktop app with Golang and Wails"
date: 2026-05-01 00:00:00 
tags: [Tutorials]
categories: [Tutorials]
---



Building a desktop application with Go may seem unusual at first, but with **Wails**, it becomes a clean and efficient approach. You get the power of Go for your backend and the flexibility of web technologies for your UI.

This tutorial walks you through creating a modern desktop application using **Golang + Wails + a web frontend**.

---

## What is Wails?

Wails is a framework that allows you to build desktop applications using:

* Go for backend logic
* HTML, CSS, and JavaScript for the frontend

Unlike Electron, Wails does not bundle a full Chromium browser, making applications **lighter and more efficient**.

<!-- IMAGE: comparison Wails vs Electron -->

---

## Prerequisites

Before getting started, make sure you have:

* Go installed (`>= 1.18`)
* Node.js installed
* Wails CLI installed

### Install Wails

```bash
go install github.com/wailsapp/wails/v2/cmd/wails@latest
```

Then run:

```bash
wails doctor
```

This command checks your environment and ensures everything is properly configured.

![wails doctor example](/assets/images/wails_doctor.png)

---

## Creating a new project

Initialize a new Wails project:

```bash
wails init -n tutorial
cd tutorial
```

You will get a structure similar to:

```
tutorial/
├── frontend/
├── app.go
├── main.go
└── wails.json
```
![tree_wails](/assets/images/tree_wails.png)

---

## Running the application

Start the development environment:

```bash
wails dev
```

This will:

* Launch the Go backend
* Start the frontend dev server


![application's running](/assets/images/application_running_wails.png)

---

## Backend in Go

Edit `app.go` to define your application logic:

```go
type App struct {
    ctx context.Context
}

func NewApp() *App {
    return &App{}
}

func (a *App) startup(ctx context.Context) {
	a.ctx = ctx
}

func (a *App) Greet(name string) string {
    return fmt.Sprintf("Hello %s!", name)
}
```

---

## Communication between Go and the frontend

Wails allows you to call Go functions directly from JavaScript without setting up an API.

Frontend example:

```javascript
import { Greet } from "../wailsjs/go/main/App";

Greet("John").then((result) => {
  console.log(result);
});
```

This removes the need for REST or RPC layers in many cases.

---

## Frontend options

You can use any frontend stack you prefer:

* Vanilla JavaScript
* React
* Vue
* Svelte

Wails provides a basic template to get started quickly.

Example:

```html
<button onclick="greet()">Say Hello</button>
```

---

## Building the application

To create a production build:

```bash
wails build
```

This generates a native executable for your operating system.

![wails build](/assets/images/wails_build.png)

---


## Conclusion

Wails is a strong alternative to Electron if you are looking for:

* Better performance
* Smaller application size
* Native integration with Go

---
