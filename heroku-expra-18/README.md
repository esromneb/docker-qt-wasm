# Instructions
From this directory:
```bash
heroku create
```

# Build
Build the docker with
```bash
heroku container:push web --app still-atoll-35873
```

# Release
Release with
```bash
heroku container:release web --app still-atoll-35873
```

Note that the binary in the CMD at the end of the docker should not exit





# See Also
* https://devcenter.heroku.com/articles/container-registry-and-runtime
* https://github.com/fiorix/freegeoip/issues/171#issuecomment-299704440