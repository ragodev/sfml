Go Binding for SFML [[Doc]](https://godoc.org/gitlab.com/tapir/sfml/v2.3/sfml)
=================

* These bindings are crafted to use Go idioms wherever possible.
* When a function is overloaded (like in class constructors) the one that makes the most sense is used as default but the other ones are also provided as secondary methods if possible.
* Class deconstructors are called automatically with ***runtime.SetFinalizer***
* Types like ***Rect***, ***Vector*** and ***Color*** are passed by value.
* Generic types are implemented with the designation of the type at the end like ***Recti***, ***Rectf***, ***Vector2f*** etc...
* Enumarations are upper camel case.
* Interfaces are used when possible to make functions like ***draw*** more generic.
* Only unicode version of the same functions are used.
* Functions return ***nil*** when there is an error because SFML doesn't have error messages.

Installation
---------------
* Make sure you have a working ***gcc*** environment and that it's in your ***PATH***.
* Copy SFML and CSFML libraries and include files to appropriate places.
* Run `go get gitlab.com/tapir/sfml/v2.3/sfml`

Status
---------
* **Window module:** 100% implemented
* **Graphics module:** 99% implemented
* **Audio module:** 80% implemented
* **Network module:** Won't be implemented. Use Go standard library instead.
* **System module:** Won't be implemented. Use Go standard library instead.
* Due to Go timer functions having low resolution on Windows, you can use [utime](https://gitlab.com/tapir/utime).

Example
------------
```go
package main

import (
    "github.com/zyedidia/sfml/v2.3/sfml""
    "runtime"
)

func init() {
	runtime.LockOSThread()
}

func main() {
	window := sfml.NewRenderWindow(sfml.VideoMode{800, 600, 32}, "Test", sfml.StyleDefault, nil)
	texture := sfml.NewTexture("test.png")
	sprite := sfml.NewSprite(texture)
	font := sfml.NewFont("arial.ttf")
	text := sfml.NewText("Hello SFML", font, 50)
    music := sfml.NewMusic("test.ogg")
    music.Play()

	for window.IsOpen() {
		if event := window.PollEvent(); event != nil {
			switch event.Type {
			case sfml.EventClosed:
				window.Close()
			}
		}
		window.Clear(sfml.ColorBlack)
		window.Draw(sprite)
		window.Draw(text)
		window.Display()
	}
}
```
