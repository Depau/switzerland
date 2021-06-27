# SIGWINCH compatibility wrapper

It's called Switzerland because only Windows really needs this, so it's WinCH. Do you like my puns?

It enables an application to use an `os.Signal`-like interface to be notified when the terminal window has been resized.

- On Unix-like systems:
  - It binds a `SIGWINCH` handler as usual
- On Windows:
  - It polls the window size regularly and notifies when a change is detected

## Usage

Sample usage without this library - works only on Unix-like systems:

```go
winch := make(chan os.Signal)
signal.Notify(winch, syscall.SIGWINCH)
defer signal.Stop(winch)
defer close(winch)
```

Sample usage with this library - multiplatform, works on Unix and Windows:

```go
winch := make(chan switzerland.WinchSignal)
switz := switzerland.GetSwitzerland()
switz.Notify(winch)
defer switz.Stop(winch)
defer close(winch)
```

## License

MIT

