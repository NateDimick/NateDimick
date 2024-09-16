# I'm Nate and Sometimes I Actually Write Code

... And when I do, it's either on company time or it ends up here.

Key descriptors about me:

* Gopher 
  * ![party gopher](https://cultofthepartyparrot.com/guests/hd/partygopher.gif)
* [(Cult of the Party Parrot Follower)](https://cultofthepartyparrot.com/)
* Primarily a backend engineer, but 🧡 cool frontend technologies like Svelete, Wails and HTMX
* I enjoy challenges and mastering new technologies
* I think Java is icky
* I think Python is icky without type hints
* I prefer TS over JS but hate how complicated the build configs are
* I have a little portfolio site with some other factoids: [natedimick.com](https://natedimick.com)

![Top Languages Card](https://github-readme-stats.vercel.app/api/top-langs/?username=NateDimick&layout=compact&theme=gotham&hide=html)

![Github Stats](https://github-readme-stats.vercel.app/api?username=NateDimick&show_icons=true&theme=gotham)

## Go Style Guide

These are my personal rules for writing good go. It will evolve over time.

### Formatting

`go fmt` includes the only style rules for go that should be applied to any project. Additional rules add unnecessary pain. `go fmt` should always be applied to all checked-in code.

### Style

* `new(type)` is always preferred over `&type{}` when allocating an empty struct. When the struct is populated, `&type{key: value}` is preferred.
* `any` is preferred over `interface{}` when defining types

* When a function returns only an error, it should be checked for inline. Example:

```go
if err := json.Unmarshal(myBytes, &myStruct); err != nil {
  //handle the error
}
```

This is also preferred for if/else statements where a value is returned by the function, but is not used outside of the if/else block

* Struct comments should be inline with the field, not above.
* Structs should never have getters or setters, unless they do something manipulative besides getting and setting
* interface definitions should always include named parameters
* named return values should only be used when a return value may be modified in a deferred statement.
* never naked return with named returns

### Patterns 

* The best way to apply configuration is through the functional configuration model. Example:

```go
func NewThing(opts ...func(*Config) *Thing {
  cfg := defaultConfig
  for _, fn := range opts {
    fn(cfg)
  }
  // finish config and return
}
```

* passing values through `context.Context` is a bad idea and should never be done. Use more explicit method of data transfer.
