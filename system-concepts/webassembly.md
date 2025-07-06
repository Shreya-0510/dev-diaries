## WebAssembly

---

### What I thought before

I had no idea what WebAssembly really meant. I just saw the term around but never looked into it.

If I had to guess back then, I probably would’ve thought it was something related to how browsers assemble different pieces like HTML, CSS, and JS and display them — kind of like rendering a complete web page.

But now that I’ve looked into it, here’s what I’ve understood.

---

### What it actually is

WebAssembly (Wasm) is a way to run **compiled code** (like from C, C++, Rust, C#) **inside the browser**.

The whole point is performance. Some stuff is just too heavy or slow in JavaScript — like games, video editing, simulations, image editing, etc. So instead of doing everything in JavaScript, you write that heavy logic in a faster language, compile it into a `.wasm` file (a binary file), and run that in your browser app.

---

### Where JavaScript fits in

WebAssembly can’t directly access or modify the DOM. So if your compiled code needs to interact with the UI or the HTML structure, **JavaScript acts as a bridge**.

So:

* WebAssembly handles the performance-heavy logic
* JavaScript handles the DOM and user interface side

---

### A breakdown that clicked for me

While trying to understand how `.wasm` is actually used in the browser, I had this realization — it felt like we were calling some method on something called `WebAssembly`. That made me think:

> Is WebAssembly an API?

Turns out, yes — it’s a built-in browser API.

WebAssembly.instantiateStreaming(fetch("file.wasm"))

Here’s what’s going on in that line:

* `WebAssembly` is the API.
* `.instantiateStreaming()` is a method of that API.
* Inside it, `fetch("file.wasm")` is just a regular fetch call.
* It loads the binary `.wasm` file, compiles it, and makes it ready to run.

So yeah, we’re basically **fetching a pre-compiled binary file** and injecting it into our browser app for performance reasons.

---

### A small detail that made sense

There’s another method called `.instantiate()` — which still works, but here’s the difference:

* With `.instantiate()`, the browser waits until the entire `.wasm` file is downloaded and read, then starts compiling.
* With `.instantiateStreaming()`, it starts compiling while the file is still downloading.

So it’s just faster and more efficient.

---

### A real-world example I imagined

Let’s say I’m building a massive educational website with:

* high-quality video content
* interactive 3D games
* art/design tools like Canva or Figma

I could write those heavier parts (like graphics rendering or game logic) in C++ or C#, compile that to `.wasm`, and load it in the browser using WebAssembly. JavaScript would handle the UI and DOM stuff.

That way, the performance-sensitive features are fast and smooth, and the UI remains interactive and clean.

---

### Summary

* WebAssembly helps run compiled code from languages like C, C++, C#, or Rust inside the browser.
* It’s useful when performance is a priority — for things JavaScript isn’t great at.
* It works *alongside* JavaScript, not instead of it.
* WebAssembly can’t directly touch the DOM — JavaScript handles that.
* The browser gives a native WebAssembly API for loading and running `.wasm` files.
* `instantiateStreaming(fetch(...))` is the better way to do it — compiles while downloading.


