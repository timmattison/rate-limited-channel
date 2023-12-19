# Rate limited channel

This is a simple rate limited channel implementation in Go. You give it an input channel and a delay and it will send
the most recent value from the input channel after the delay has passed.

# What can it be used for?

I wrote this when I started working on projects with [Bubble Tea](https://github.com/charmbracelet/bubbletea). I had
some processes that wrote status information to a channel and I wanted to display the most recent status information
in my TUI.

I didn't want to display every single status update because the data sometimes comes in too fast (many updates per
second).

I also didn't want to couple the producer to the TUI.

I just wanted to be able to configure how often I could get updates from the producer.

So now I can take the `fastChannel` and say I want to get updates at most every 100 milliseconds like this:

```go
  tuiUpdateChannel := rate_limited_channel.ToRateLimitedChannel(fastChannel, 100*time.Millisecond)
```
