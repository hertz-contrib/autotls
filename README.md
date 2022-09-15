# autotls


Support [Let's Encrypt](https://letsencrypt.org/) for Hertz.

# How to start it

1. Prepare a VM and a domain.
2. Create a new DNS A record targeting your VM public IP.
3. Write code and compile it.
4. Start the binary.
5. Open your browser with the address of your DNS domain.

# Example

```Go
func main() {
	h := server.Default(
		server.WithTLS(autotls.NewTlsConfig("your domain")), 
		server.WithHostPorts(":https"),
	)

	// Ping handler
	h.GET("/ping", func(c context.Context, ctx *app.RequestContext) {
		ctx.JSON(200, map[string]interface{}{
			"ping": "pong",
		})
	})

	hlog.Fatal(autotls.Run(h))
}
```

More examples can be found in the [examples](./examples) directory.