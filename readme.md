# docker-password-store

Run password-store inside of a Docker container.

I built this so I could ensure that I am able to import my PGP private key and
password store in case my laptop catches fire, falls into a lake, and is eaten
by an alligator...

## Instructions

Make sure that your `.gnupg/gpg-agent.conf` has only the following line for
`pinentry-program`:

```
pinentry-program /usr/bin/pinentry-curses
```

### Download and run password-store image

(from local machine)

```sh
# download password-store Docker image
docker pull audy/password-store

# start bash in password-store image with the necessary directories mounted
docker run \
  -ti \
  --rm \
  --volume $HOME/.password-store:/root/.password-store \
  --volume $HOME/.gnupg:/root/.gnupg \
  audy/password-store \
  /bin/bash

# alternatively, just print a password
docker run \
  -ti \
  --rm \
  --volume $HOME/.password-store:/root/.password-store \
  --volume $HOME/.gnupg:/root/.gnupg \
  audy/password-store \
  pass github
```

### Test decryption of passwords.

(inside of running Docker container)

```sh
pass ls # list passwords

pass github # print github password to STDOUT
```

## License

The MIT License (MIT)
Copyright (c) 2015 Austin Davis-Richardson

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
